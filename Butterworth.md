# Butterworth Low-Pass Filter Design (MATLAB)

## Objective
Design a low-pass Butterworth IIR filter based on given passband and stopband specifications.

---

## Specifications
- Passband cutoff frequency: 0.2π  
- Stopband cutoff frequency: 0.3π  
- Passband ripple (Rp): 7 dB  
- Stopband attenuation (As): 16 dB  

---

## Methodology

- Defined normalized passband and stopband frequencies in MATLAB.
- Used `buttord` to compute the minimum filter order (N) and cutoff frequency (Wn).
- Designed the Butterworth low-pass filter using the `butter` function.
- Obtained numerator (b) and denominator (a) coefficients of the IIR filter.
- Plotted magnitude and phase response using `freqz`.

---

## MATLAB Code

```matlab
clc; clear; close all;

wp = 0.2;    
ws = 0.3;   
Rp = 7;      
As = 16;     

[N, Wn] = buttord(wp, ws, Rp, As); 
[b, a] = butter(N, Wn, 'low'); 

disp(['Filter Order N = ', num2str(N)]);
disp(['Cutoff Frequency Wn = ', num2str(Wn)]);

freqz(b, a, 1024);
