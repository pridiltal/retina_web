---
authors:
- admin
categories: []
date: "2021-11-09"
draft: false
featured: false
image:
  caption: "Image credit: pixabay"
  focal_point: ""
lastMod: "2023-06-26"
projects: []
subtitle: 
summary: 
math: true
tags: 
- RETINA
title: 'Anomaly Detection in Image Time Series Using Explainable AI (XAI)'
---

## Anomaly Detection in Image Time Series Using Explainable AI (XAI)

Analysis of Image time series (ITS) has become increasingly important as a tool for monitoring and
understanding complex systems and phenomena, such as climate change, urbanization, and land-use changes.
By capturing images at regular intervals, it is possible to track and analyze changes and trends over time, which can help inform decision-making and policy development. The existing deep learning-based anomaly
detection methods solely focus on the classification task, leading to a lack of explainability in the model and reducing human trust in the system. We proposed a framework for early detection of anomalies in image
time series using explainable AI, which defines an anomaly as an observation that is very unlikely given
the forecast distribution for the corresponding time period. Our previous study focused on developing the
entire framework for detecting anomalies in image time series. In this work, our attention is on further
improving the explainable AI component of the proposed framework. Our proposed framework consists
of a deep learning-based computer vision module that derives a feature space from the ITS data, a deep
learning-based time series forecasting module that generates a probability distribution for each time period, and an extreme value theory-based boundary prediction process that helps identify anomalies. To address the lack of transparency and interpretability in the deep learning-based anomaly detection component, we integrate an explainable AI (XAI) module that provides post-hoc, model-agnostic, and local explanations, increasing the trustworthiness of the prediction of anomalous behaviours. Our experiments with satellite image time series (SITS) show that the proposed algorithm can work well even in the presence of noisy image time series data and that the XAI module improves the transparency and interpretability of the deep learning-based anomaly detection framework. Overall, our proposed framework provides a powerful tool for detecting the progression of unusual behaviours in ITS with increased trustworthiness and interpretability and has a wide range of applications in environmental monitoring, disaster management, and climate change analysis.

[Slides](talks/ISF2023/ISF_2023.html)


