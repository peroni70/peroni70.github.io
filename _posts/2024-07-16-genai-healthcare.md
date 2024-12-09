---
title: 'Deep Generative Models for Healthcare'
date: 2024-11-16
permalink: /posts/2024/11/deep-gen-health/
bibliography: test.bib
# layout: distill
tags:
  - Healthcare
  - ML
---


![](/images/brain.gif)
# Introduction

While major strides have been made in deep generative modeling, including significant advances in natural language, image, and video generation, there remains a disconnect between these technical advances and practical applications, especially for social good. A critical application area for deep learning is healthcare, where high-stakes decision-making occurs daily and learning algorithms can directly improve lives. In my own research, and in the broader machine learning for healthcare community, the focus has largely been on discriminative and prescriptive modeling. These approaches are directly motivated by the problems encountered in health applications, such as predicting the risk of developing a disease, predicting whether a scan includes a tumor, or prescribing the best treatment to maximize patient outcomes. Recently, language-based generative models have gained traction as a practically useful tool in healthcare tasks, assisting with summarization, feature extraction, and even structured prediction [CITE popular healthcare foundation models]. The flexibility of natural language, along with the impressive zero-shot and in-context learning ability of these models, allows them to perform a large variety of useful tasks. However, the motivation for image-based generative modeling in health applications is less clear. 

How might we use generated images to improve healthcare operations and outcomes? Image data is ubiquitous in healthcare, from X-Rays to MRIs and CT scans, to histopathology (microsopic imaging of tissue and cells). However, unlike other applications, image data in healthcare is highly specific to each patient, and "creativity" in the image output would be highly discouraged. Therefore, image-based generative models for healthcare must provide either significant discriminative ability or be carefully conditioned on existing patient data. That is, there are two primary avenues for image-based generative models to improve healthcare:

1. __Image Reconstruction.__ Due to how expensive and time-consuming certain imaging techniques are, such as MRIs and CT scans, it has become important to downsample or sparsify the measurements taken for these images. As a result, the inverse problem of reconstructing the true image from the partial measurements is ill-posed, making reconstruction a challenging task. This is naturally a conditional image generation problem.

2. __Public Synthetic Dataset Generation.__ An acute problem in ML for healthcare is the accessibility and availability of patient data. Patient data is traditionally kept on-premise within  hospital networks, necessitating all research be conducted with the compute resources available within those individual networks. In practice, this dramatically slows the rate of research and development, as researchers wrestle with high latency, antiquated hardware, small datasets, and limited compute resources. There is therefore an exciting and promising direction for generative modeling to resolve this problem by allowing us to generate synthetic data, which could potentially be used outside of the hospital networks.

# Solving Inverse Problems with Generative Models
At a high-level, we can pose the image reconstruction problem for medical images as follows: let \\(y \in \mathbb{R}^m\\) be some low-dimensional representation of a raw input image $x \in \mathbb{R}^n$, generated by the linear transformation $y = Ax + \epsilon$ where $A \in \mathbb{R}^{m \times n}$ and $\epsilon \in \mathbb{R}^m$ is a noise vector. That is, $y$ is a noisy projection of the raw input image $x$ onto a lower-dimensional space. Our goal, ultimately, is to collect only the lower-dimensional measurements $y$ and solve the inverse problem to recover the most likely full image $x$ corresponding to $y$. This can save patient time, improve patient safety, and reduce hospital costs. For a given transformation $T: x \rightarrow Ax + \epsilon$, this inverse problem can be treated as a supervised learning problem, for which we have pairs $\{(x_i, y_i)\}_{i=1}^N$ of images and their corresponding projections [CITE]. However, in practice, this transformation can vary significantly, even for the same type of image. For example, one hospital might be taking $m=10$ measurements, while another hospital might be taking $m=25$ measurements. The transformation matrix $A$ applied may also be different, separate from the number of measurements. This would require generating pairs of measurements and raw image data for each physical machine creating this data.

Rather than thinking of this as a supervised learning problem, [CITE Song paper] propose addressing this problem with unconditional image generation. The key, as we will soon discuss, is to guide the image generation at inference time by nudging the generated image toward satisfying the condition $y = Ax$, where $y$ is the actual measurements, and $x$ is the generated image. The first step is __training an unconditional score model__ $s_{\theta^*}(x, t)$ on a dataset of full images (e.g. CT scans or MRIs). At inference, we expect to only have some measurements $y$, for which we can generate a conditional stochastic process $\{y_t | y\}_{t \in [0,1]}$ by using the linear relationship,
$$y_0 = Ax_0 + \epsilon = y,$$
and, noting that $x_t \sim \mathcal{N}(\alpha(t)x_0, \beta(t)^2I)$, we can derive the relation
$$y_t = \alpha(t)y + \beta(t)Az,$$
where $z \sim \mathcal{N}(0,I)$ and $\alpha(t), \beta(t)$ are noise schedules. Therefore, $y_t$ is an interpolation between the true measurements $y$ and noise $z$ that has been projected to the same space as $y$ through the transformation matrix $A$.

From this point, the traditional iterative sampling process would sample timesteps $\{0=t_1 < t_2 < \dots < t_n=1\}$ and produce observations 
$$x_{t_{i-1}} = h(x_{t_i}, z_i, s_{\theta^*}(x_{t_i}, t_i))$$
where $h$ could be given by the Euler-Maruyama sampler,
$$h(x_{t_i}, z_i, s_{\theta^*}(x_{t_i}, t_i)) = x_{t_i} - f(t_i)x_{t_i}/N + g(t_i)^2s_{\theta^*}(x_{t_i}, t_i)/N + g(t_i)z_i/\sqrt{N}.$$
In their work, [CITE song] propose an additional step in this denoising process that corrects for the measurement process,
$$x_{t_i}' = k(x_{t_i}, y_{t_i}, \lambda)$$
$$x_{t_{i-1}} = h(x_{t_i}', z_i, s_{\theta^*}(x_{t_i}, t_i))$$
where, critically, the function $k$ solves a proximal optimization step that aims to minimize the distance between $x_{t_i}$ and $x_{t_i}'$ while also minimizing the distance between $x_{t_i}'$ and the hyperplane $\{x \in \mathbb{R}^n | Ax = y_{t_i}\}$. That is, $x_{t_i}'$ should be a projection of $x_{t_i}$ onto the feasible set $\{x \in \mathbb{R}^n | Ax = y_{t_i}\}$. With the hyperparameter $\lambda \in [0,1]$, the optimization problem becomes
$$x_{t_i}' = \text{argmin}_{z \in \mathbb{R}^n} \; (1-\lambda)||z - x_{t_i}||^2 + \lambda\min_{u \in \mathbb{R}^n}||z - u||^2 \quad \text{s.t.} \quad Au = y_{t_i}$$
where $\lambda$ controls the relative importance of the two objectives. Notice when $\lambda = 1$, we guarantee that $x_{t_i}'$ satisfies $Ax_{t_i}' = y_{t_i}$. In practice, the authors use Bayesian optimization to tune this hyperparameter empirically. Using a decomposition for the transform matrix $A$ (which only assumes $A$ is full rank), the authors are able to derive a closed form solution for $k$, such that this step is both exact and efficient. A visualization of this process is given below

[INSERT VISUAL]

At this point in time, this approach represents the state of the art in solving such inverse problems, even matching or outperforming supervised learning approaches while providing significant flexibility. In my opinion, this idea of guiding unconditional genertive models at inference is extremely promising for a variety of applications, but especially in healthcare, where labeled data is less readily available and conditions change across different hospital systems. 

[INSERT VISUAL BRAINS]

Coming from a background in Operations Research, the proximal optimization step that guides the image generation is particularly interesting. While the authors do not provide this ablation study, I would be curious to see how the generated images change qualitatively for varying values of $\lambda$. It is possible that when $\lambda=1$, the resulting image $x_{t_i}'$ looks somewhat unrealistic. Recall that when $\lambda=1$, the generated image $x_{t_i}'$ is a projection of $x_{t_i}$ onto the hyperplane $\{x \in \mathbb{R}^n | Ax = y_{t_i}\}$. While this point may be the closest in space to $x_{t_i}$ that satifies the measurement process, it may be that this point contains unrealistic artifacts. Instead, an alternative approach could be to follow a path from $x_{t_i}$ to the feasible hyperplane that maximizes the likelihood of $x_{t_i}'$. Given that we don't typically have access to the marginal distribution $p_t(x_t)$, we could instead find a path along which the score function is maximized. More formally, suppose we have a current sample $x_t$ with a corresponding measurement $y_t$. Then maximizing the score along some path $\gamma$ from $x_t$ to the hyperplane $Au = y_t$ at some point $x_t'$ gives us

$$
\max_{x_t' : Ax_t' = y_t}\int_\gamma \nabla_x \log(p(x)) dx = \max_{x_t' : Ax_t' = y_t} \log(p(x_t')).
$$

However, we don't typically have access to $p(x_t')$, but we do have access to $s_{\theta^*}(x_{t}, t) \approx \nabla_{x_t}\log(p(x_t))$, which we can use to recover a path that increases $p(x_t')$.

While likely less efficient than the proximal update step, which has a closed-form solution, there are multiple ways that this formulation could be approximately solved. For example, discretizing the space between $x_{t_i}$ and the feasible hyperplane, one could evaluate the score function at each grid point and then solve a shortest path problem to find a path that maximizes the total score. Alternatively, one could follow an iterative approach, where at each step the score function $s_t = s_{\theta^*}(x_{t_i}, t_i)$ is evaluated, the resulting gradient vector is filtered such that only the components in the direction of the feasible hyperplane are kept, and $x_{t_i}$ is updated in the direction of this vector. That is, suppose $\mathbf{n}_t$ is the normal vector to the hyperplane $Au = y_t$, then we would do
$$s_{proj}(x_t, t) =  s_{\theta^*}(x_{t}, t) \odot (s_{\theta^*}(x_{t}, t) \odot \mathbf{n}_t > 0.)$$
$$ x_t' \leftarrow x_t' + \eta \cdot s_{proj}(x_t, t)$$
Where $\eta$ is our step-size, and $s_{proj}(x_t, t)$ selects the components of $s_{\theta^*}(x_{t}, t)$ that are in the direction of the feasible hyperplane. In the case $||s_{proj}(x_t, t)|| \approx 0$, we could default to the proximal step. This process could be repeated multiple times until $x_t'$ approximately satisfies the measurment constraints. Crucially, such approaches would eliminate the need for the sensitive hyperparameter $\lambda$, and may produce higher quality results.

## Extension to Consistency Models

One drawback of the score matching diffusion models described in the previous section is that inference is often quite slow due to the many iterations involved in the generation process. Further modifications to the generation process, such as the additional update steps proposed, and especially the steps I suggested as future work, would only slow down this process further. The recently developed Consistency Models [CITE song] offer an alternative few-step diffusion approach that achieves impressive performance using a fraction of iterations required for traditional diffusion models. While a sufficient introduction to Consistency Models is outside the scope of this blog, at a high level

[FIll IN]

Notice, however, that the process used to generate images at inference is quite similar, visually, to the guided process for generating images in the previous section. In fact, such a proximal optimization step can be easily incorporated into the Consistency Model framework. In their work, Song describe such an approach as zero-shot image editing. The model itself would be trained as usual, to perform unconditional image generation. Then, at each step of the sampling process, prior to adding noise, we apply the proximal optimization step as defined in the previous section. This would achieve the same goal of guiding the generation process according to the measurements, but it would do so with only a few iterations. 

# Public Synthetic Dataset Generation
We now turn our attention to the other major area for generative image models in healthcare - creating __useful, anonymized__ synthetic datasets. These two terms, useful and anonymized, characterize the necessary conditions for such image generation in healthcare.

## Differentially Private SGD