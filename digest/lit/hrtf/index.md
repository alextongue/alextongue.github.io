---
title: HRTF
layout: default
nav_order: 3
parent: Literature
has_children: true
has_toc: false
date: 2020-05-14
---

# Head Related Transfer Functions

*(for references, please check out the [Immersive Sound](https://alextongue.github.io/digest/lit/2019-09-16-initial.html) textook that I had mentioned earlier)*

Humans are able to localize external acoustic stimuli through the interaction of incident acoustic stimuli on their bodies, namely the head and torso. A **Head-Related Transfer Function (HRTF)** characterizes these differences in the form of a conventional linear transfer function. This transfer function contains two types of binaural[^1] cues or differences:

- **Interaural Time Difference (ITD):** Sound from different azimuthal directions[^2] arrive at each ear at different times. This is due to the location of the ears on opposite sides of the head, and is primarily perceptible at lower frequencies (longer wavelengths; <4 kHz[^3]). 
- **Interaural Intensity Difference (IID) or Interaural Level Difference (ILD):**
  - Sound from different elevation directions[^4] plane arrive at each ear at different intensities. This is due to the complex geometry of the ear pinnae and is highly frequency dependent. Primarily, there is a notch filter that changes in frequency for different elevations (5 kHz to 10 kHz)
  - Sound from different azimuthal directions arrive at each ear at different intensities. This is due to the head and torso absorbing energy (known as the shadowing effect), and is primarily perceptible at higher frequencies (>2 kHz). 

These linear spectral distortion and time delays can be sufficiently expressed as a collection of FIR filters and stored as a $M \times 2 \times N$ matrix, where $M$ is the number of locations sampled and $N$ is the length of the filter.

Location coordinates are commonly stored in a $M \times 3$ companion matrix. The basis vectors are either spherical $(\theta,\phi,r)$ or cartesian $(x,y,z)$.

The ITD time delays are either directly incorporated in the impulse response itself or as a floating-point number in a separate $M \times 2$ matrix.

## Footnotes

[^1]: related to two ears
[^2]: azimuthal meaning horizontal; the azimuthal plane divides the head into top and bottom halves
[^3]: This is for broadband signals. For more contrived pure sinusoids, the upper frequency limit is lower.
[^4]: elevation meaning vertical; the vertical plane divides the head into left and right halves