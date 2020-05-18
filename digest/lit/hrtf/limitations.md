---
title: Limitations
nav_order: 2
parent: HRTF
grand_parent: Literature
has_toc: false
---

# HRTF Limitations

As of now, there are several types of limitations in using HRTFs:

### Acquisition

The most straightforward way to capture an individual HRTF is through direct acoustic measurement. An acoustic stimulus is played back from a known direction and recorded by microphones placed in the ear canal of the subject. Direct measurement, however, is costly, requiring
- equipment for stimulus playback, capture, and accurate head-tracking
- a sufficiently-large environment with known acoustic properties, and
- subject and administrator time for the actual measurement to take place.

Generic HRTFs have been statistically derived, either through databases or measuring "dummy-head" head-and-torso simulators (HATS),which themselves have been constructed from standardized median head measurements. These have shown to provide some amount of localization, but it has been shown that individualized HRTFs are more successful in externalizing sound.

### Storage and Computation

An additional constraint in systems that incorporate HRTFs is the storage and fast retrieval of large datasets. Applying a single FIR filter to an audio stream only requires either one time-domain convolution or a set of DFT[^1] computation, frequency multiplication, and inverse DFT computation. However, the computational load rises exponentially for systems that require processing of different audio rays through multiple HRTF filters in real-time, in order to convincingly convey virtual spatial environments.

## Solutions

Several notable advances in HRTF acquisition and computation include the following:

- Acoustic reciprocity holds in HRTF capture, which allows for speakers to be placed in the ears, which in turn allows multiple microphones to be placed around the ear for the capture of multiple points with one stimulus [^2].
- Boundary-element modeling (BEM) methods that simulate the acoustic absorption, reflection, and diffraction that takes place in an HRTF. If implemented correctly, this only requires an accurate model of a subject's head and torso, which can employ 3D scanning techniques or computer vision. This results in a reduction of measurement time, but higher offline computational time and a different cost of equipment (cameras and scanners) [^3].
- There has been a notable effort in estimating HRTFs. This involves finding correlations between different HRTF features based on non-acoustic data, such as anthropomorphic measurements of the head and torso. This allows for HRTF computation to be bridged with the fields of statistical learning and machine learning, which has been a rapidly growing field as of the past decade. These interpolation techniques will be summarized in a separate post.

## Footnotes

[^1]: Discrete Fourier Transform; this is most efficiently implemented through the Fast Fourier Transform (FFT) algorithm
[^2]: [https://doi.org/10.1121/1.2207578](https://doi.org/10.1121/1.2207578)
[^3]: Ziegelwanger, H., and Kreuzer, W., Majdak, P. (2015). "Mesh2HRTF: An open-source software package for the numerical calculation of head-related transfer functions," in *Proceedings of the 22nd International Congress on Sound and Vibration*, Florence, IT.

