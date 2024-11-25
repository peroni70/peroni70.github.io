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

2. __Dataset Generation.__ An acute problem in ML for healthcare is the accessibility and availability of patient data. Patient data is traditionally kept on-premise within the hospital's network, necessitating all research be conducted with the compute resources available within that network. In practice, this dramatically slows the rate of research and development, as researchers wrestle with high latency, antiquated hardware, and limited compute resources. There is therefore an exciting and promising direction for generative modeling to resolve this problem by allowing us to generate synthetic data, which could potentially be used outside of the hospital networks.



# Differentially Private SGD