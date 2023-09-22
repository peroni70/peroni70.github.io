---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

Education
======
* Ph.D. in Operations Research, Massachusetts Institute of Technology, expected 2025
  * Advised by Professor Dimitris Bertsimas
  * Research Topics: Machine Learning for Healthcare, Interpretable Deep Learning, Multi-modal Machine Learning
  * GPA 5.0/5.0
* B.A. in Mathematics with Honors, Cornell University, 2020
  * Concentration in Applied Math, Minor in Computer Science

Research
======
For my Ph.D., I am advised by Professor Dimitris Bertsimas, working broadly on machine learning for high-stakes decision-making, specifically in the healthcare domain. My current work includes the following topics:
 * __Interpretable Deep Learning__ - Developing new methods and model architectures
to create inherently intelligble deep learning model, with a focus on healthcare
applications.
 * [__Multi-Modal AI for Healthcare__](https://hartfordhealthcare.org/about-us/innovation/mit) - Leading architecture and engineering development of HAIM 2.0, a multi-modal ML framework for creating models that integrate
many data modalities often found in healthcare data. Serve as point-of-contact for
our Hospital partners regarding data and compute infrastructure, encompassing 14 ongoing
research projects.
* __Model Selection and Deferral__ - Developing methods for selecting which ML models to use, and when to defer to human judgment, in high-stakes decision-making
scenarios.

Work experience
======
* __Machine Learning Engineer - Enolink Technologies, Cambridge, MA (September 2021 - September 2022)__
  * Develop, deploy, and scale risk models for clinical decision support systems that are currently in use at Hospitals in South Korea. Owned end-to-end development of new features from model experimentation to infrastructure and platform engineering, model serving and backend development.
   * Led research efforts for interpretability and explainability methods for risk models within the company, developing novel interpretable deep learning methods for survival analysis that have been submitted to Machine Learning for Health 2022 (that match the accuracy of state-of-the-art models while preserving interpretability).
  * Led engineering for the company’s first product pilot launch, which included: 
    * Automating application deployment to both AWS environments and the hospital network using Ansible, Kubernetes, and Gitlab CI/CD
    * Implementing performance improvements for the API and model serving, reducing response/inference time by an order of magnitude (O(10s) to O(1s))
    * Upgrading logging aggregation by integrating Loki/Grafana
    * Upgrading data pipelines
    * Conducting weekly meetings with clinicians and hospital IT staff
  * Built the backend for one of our primary clinical decision support applications, including features to surface model predictions, generate (SHAP) model explanations and simulation results, and provide integrations with our data pipeline to yield patient information.
  * Designed and implemented functionality to serve SHAP model explanations stratified by patient cohort, enabling more precise risk assesments.
  * Conducted behavioral and technical interviews with candidates for full-time machine learning engineer roles.


* __Software Engineer, Machine Learning -  Capital One, Cambridge, MA (August 2020 - September 2021)__
  * Developing a suite of semantic recommendation systems with underlying NLP models to simplify and improve the experience of both finding and creating relevant and effective regulatory documents for our risk associates. 
  * Owned end-to-end development of a new intelligent search feature. Designed implementation plan, conducted experiments, documented and presented results, integrated final model selection into backend, and updated the ETL pipeline and UI.
  * Pitched and created an intelligent writing assistant tool for our domain based on a custom BERT classification model and spaCy language model for a company Hackathon. Project won 2nd place and development is being continued. 
  * Creating a Q&A information retrieval system for policy documents based on a sentence-BERT model to improve the experience of answering policy-related questions. 
  * Organized and led presentations with diverse internal audiences, covering topics such as word embedding models and deploying NLP services to production. 
  * Tech: Python, Django, Vue.js, Apache Airflow, AWS, SQL, PyTorch, Gensim, Hugging Face, spaCy, Word2Vec, sentence-BERT


* __Software Engineer Intern - Schlumberger, Houston, TX (June 2019 - August 2019)__
  * Developed a python package for predictive monitoring and analysis of processing
facilities containing nonlinear Bayesian filters, online event detection, and forecasting
for time series data.
  * Validated python package using application-specific data and demonstrated increase
in forecasting ability from 30 days to 120 days.
  * Created a full-stack dashboard to analyze online model performance with a backend
written in Go, using Google Cloud Platform for data storage and Grafana for data visualization.
  
Languages + Skills
======
My primary language for development is __Python__, but I also have some professional experience with Go. I also have experience with functional programming in OCaml (not professionally) and greatly enjoy working with this paradigm.

* __Python__
  * Experienced using and developing data science, statistics, and machine learning libraries
  * Develop APIs with Django/Flask
  * Data Engineering with Airflow + Dask
* __Go__ 
  * Experience developing Golang-based AWS Lambdas
* SQL
  * Used as needed on data projects (moderate skill)
* Java, OCaml
  * Non-professional experience during college, not recently used
* Deployment + CI/CD: Docker, K8s, AWS (SA Certified), Git, Gitlab CI/CD

### Machine Learning Skills
While a lot of my knowledge and experience in building ML systems comes from working on a variety of awesome projects in industry (mentioned above), I've also sat down and cranked out the math in a variety of courses, such as [Unsupervised Learning]((https://www.cs.cornell.edu/courses/cs4786/2019sp/)), [Supervised Learning]((https://www.cs.cornell.edu/courses/cs4780/2019fa/)), (Graduate) [Foundations of Modern Machine Learnging]((https://www.cs.cornell.edu/courses/cs6781/2020sp/)), and (Graduate) Machine Learning Under a Modern Optimization Lens to name a few. My skills include:
* Interpretable ML and Explainable AI (XAI)
* NLP
  * Information Retrieval, Classification, Feature Extraction + Named-Entity Recognition, Generative Models
* Survival Analysis
* Supervised + Unsupervised Learning
  * Industry Experience +  Coursework [ [1](https://www.cs.cornell.edu/courses/cs4780/2019fa/), [2](https://www.cs.cornell.edu/courses/cs4786/2019sp/), [3](https://www.cs.cornell.edu/courses/cs6781/2020sp/) ]
* Machine Learning Optimization
* Data visualization + Model Interpretation 
* State Estimation + Anomaly Detection
* Markov Decision Processes
* Mathematical Statistics + Machine Learning Theory
  * Graduate Coursework [ [1](https://www.cs.cornell.edu/courses/cs6781/2020sp/), [2](https://pi.math.cornell.edu/m/Courses/GradCourses/fa16/6230.html), [3](https://www.cs.cornell.edu/courses/cs6840/2020sp/) ]


Publications
======

See my [Google Scholar](https://scholar.google.com/citations?hl=en&user=kvjX-dIAAAAJ) page for the most up-to-date list of publications.

Talks
======
* (Upcoming) __Interpretable NLP For Identifying Risk Factors Of Intimate Partner Violence In Clinical Notes__, INFORMS Annual Conference, October 2023, Phoenix, AZ
* __Interpretable TabText__, INFORMS Healthcare, July 2023, Toronto, Canada

Patents
======

A Discriminative Model to Identify and Demarcate Textual Features in Risk Control Documents
- Application Filed
- Submitted 8/12/2022

System for Suggesting Words, Phrases or Entities to complete sequences in Risk Control documents
- Application Filed
- Submitted 8/10/2022

Hybrid Model and System For Predicting Quality and Identifying Features and Entities of Risk Controls
- Application Filed
- Submitted 5/17/2022
  
Teaching
======
  * CS Teaching Assistant, Analysis of Algorithms, Cornell University (Fall 2019)
    * Held regular office hours review sessions, and graded problem sets and exams.
  * BEE Teaching Assistant, Bio-Fluid Mechanics, Cornell University (Fall 2018)
    * Held regular office hours and review sessions, developed problem set questions, and created a case study focusing on cardiovascular flows.
  * Tutor, Mathematics Support Center, Cornell University (Fall 2018)
   * Tutored all calculus courses, linear algebra, and differential equations
  
Projects
======
* [Semantic Movie Search](https://peroni70.github.io/posts/2021/05/movie-search-1/)
* More projects, old and new, coming soon!

Certifications
======
AWS Solutions Architect - Associate (April 2021 - April 2024)


