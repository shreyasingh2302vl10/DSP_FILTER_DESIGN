# Digital Signal Processing Filter Design and Analysis

A MATLAB-based **Digital Signal Processing (DSP)** project focused on designing and validating **low-pass IIR filters** using classical approximation and analog-to-digital conversion techniques.

---

##  Project Overview

This project includes the design and analysis of:

* **Butterworth Low-Pass IIR Filter**
* **Chebyshev Type-I Low-Pass IIR Filter**
* **Impulse Invariance based Digital Filter Design**
* **Bilinear Transformation based IIR Realization**
* **Frequency response verification using `freqz` and Filter Designer**

---

##  Design Specifications

The following specifications were used during filter design:

* **Passband cutoff:** `ωp = 0.2π`
* **Stopband cutoff:** `ωs = 0.3π`
* **Passband ripple:** `Rp = 1–7 dB`
* **Stopband attenuation:** `As = 15–16 dB`

---

##  Implemented Methods

### 1) Butterworth Filter Design

Designed smooth-response low-pass IIR filters using:

* `buttord()`
* `butter()`

### 2) Chebyshev-I Filter Design

Designed sharper transition low-pass filters with controlled ripple using:

* `cheb1ord()`
* `cheby1()`

### 3) Impulse Invariance Technique

Converted analog filter prototypes into digital IIR filters using:

* `impinvar()`

### 4) Bilinear Transformation

Implemented stable digital IIR realization using:

* `bilinear()`

---

##  Analysis and Validation

Filter performance was validated through:

* Magnitude response
* Phase response
* Passband ripple verification
* Stopband attenuation analysis
* MATLAB `freqz` plots
* Filter Designer GUI cross-check

---

##  Tools and Technologies

* **MATLAB**
* Signal Processing Toolbox
* Filter Designer

---

##  Key Learning Outcomes

* Classical **IIR filter design techniques**
* Analog-to-digital filter conversion
* Frequency-domain response analysis
* MATLAB-based DSP workflow
* Practical understanding of Butterworth and Chebyshev filters

---



