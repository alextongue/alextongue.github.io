---
title: Machine Learning
layout: default
nav_order: 3
parent: HRTF
grand_parent: Literature
has_toc: false
date: 2020-05-14
---

# HRTF Estimation using Statistical and Machine Learning

[As mentioned earlier](https://alextongue.github.io/digest/lit/hrtf/limitations.html), there are limitations in measurement and computation that make it inconvenient to easily acquire an individualized set of HRTFs. Primarily, it takes time, specialized equipment, and a controlled acoustic environment for an accurate HRTF to be measured.

There has, however been a push for HRTFs to be estimated from other features that are easier to measure. Some notable examples:

- **Tamuloionis and Serackis, 2019:** The performance of a classic perceptron has been compared with that of a cascaded feed-forward architecture to estimate the first 128 points of 256-point HRTFs given coordinates as input features. The number and size of hidden layers, as well as combinations of cartesian and spherical coordinate representations have been compared.
  - Using the ARI database (170+ subjects, 1550 HRTFs per subject), the model was trained over 300,000 epochs with momentum and "adaptive learning," although it is unclear which type of adaptive learning was used.
  - It was shown that a two-layer perceptron with intermediate layer sizes [64, 32] and tanh activation functions performed the best, yielding a derived similarity metric of an R regression value of 0.87132.
- **Kestler, Yadegari, and Nahamoo, 2019:** A network was constructed to take inputs of anthropomorphic data and cartesian coordinates and output 32-point HRTFs in decibel space, IID only.
  - The cost function used was a MSE of predicted and actual filters, both of which were mean-subtracted and normalized by variance.
  - The final result metric used was a RMSE of predicted and actual filters; this is similar to the square root of the above MSE using unnormalized data.
  - Two experiments were trained on one subject from the public CIPIC database (1250 HRTFs): the first predicted azimuthal filters at $\theta = 0\degree$ elevation, and the second predicted filters at all azimuths and elevations.
  - The third experiment was trained on 
  - For all experiments, a 10% subset was removed in the beginning for test evalutation. Using the remaining data, the network was trained over 20 epochs with with 20 iterations of 20% cross-validation, resulting in 400 forward passes. 