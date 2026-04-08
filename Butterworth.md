# Butterworth Low-Pass Filter Design (MATLAB)

This experiment demonstrates the design of a **low-pass Butterworth digital filter** using three approaches:
1. Direct Digital Design  
2. Impulse Invariance Method  
3. Bilinear Transformation Method  

---

# 1. Direct Digital Butterworth Filter

## Introduction
A low-pass Butterworth filter is designed directly in the digital domain using given specifications.  
Butterworth filters provide a **maximally flat passband response**.

## Specifications
- Passband cutoff: 0.2π  
- Stopband cutoff: 0.3π  
- Passband ripple: 7 dB  
- Stopband attenuation: 16 dB  

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
```

## Explanation
- `buttord` calculates the minimum filter order.  
- `butter` generates filter coefficients.  
- `freqz` plots magnitude and phase response.  

## Result
- A smooth low-pass response is obtained.  
- No ripple in passband.  

---

# 2. Butterworth using Impulse Invariance

## Introduction
Impulse invariance converts an **analog filter into a digital filter** by preserving the impulse response samples.

## Specifications
- Passband cutoff: 0.2π  
- Stopband cutoff: 0.3π  
- Passband ripple: 1 dB  
- Stopband attenuation: 15 dB  

## MATLAB Code
```matlab
clc; clear; close all;

wp = 0.2 * pi;
ws = 0.3 * pi;
Rp = 1;
As = 15;
T = 1;

Omega_p = wp / T;
Omega_s = ws / T;

[N, Omega_c] = buttord(Omega_p, Omega_s, Rp, As, 's');
[b, a] = butter(N, Omega_c, 's');

[bd, ad] = impinvar(b, a, 1/T);

disp(['Filter Order N = ', num2str(N)]);
disp(['Cutoff Frequency Omega_c = ', num2str(Omega_c)]);

freqz(bd, ad, 1024);
```

## Explanation
- Digital frequencies are converted into analog frequencies.  
- Analog Butterworth filter is designed.  
- `impinvar` converts analog filter to digital.  

## Result
- Desired low-pass response is achieved.  
- Some aliasing may occur at higher frequencies.  

---

# 3. Butterworth using Bilinear Transformation

## Introduction
Bilinear transformation converts an analog filter into a digital filter while **avoiding aliasing**.

## Specifications
- Passband cutoff: 0.2π  
- Stopband cutoff: 0.3π  
- Passband ripple: 1 dB  
- Stopband attenuation: 15 dB  

## MATLAB Code
```matlab
clc; clear; close all;

wp = 0.2 * pi;
ws = 0.3 * pi;
Rp = 1;
As = 15;
T = 1;

Omega_p = (2/T) * tan(wp/2);
Omega_s = (2/T) * tan(ws/2);

[N, Omega_c] = buttord(Omega_p, Omega_s, Rp, As, 's');
[b, a] = butter(N, Omega_c, 's');

[bd, ad] = bilinear(b, a, 1/T);

disp(['Filter Order N = ', num2str(N)]);
disp(['Cutoff Frequency Omega_c = ', num2str(Omega_c)]);

freqz(bd, ad, 1024);
```

## Explanation
- Pre-warping is applied using tangent function.  
- Analog filter is designed.  
- `bilinear` converts it into digital form.  

## Result
- Accurate low-pass response is obtained.  
- No aliasing occurs.  

---

# Comparison

| Method              | Advantage                  | Disadvantage            |
|--------------------|--------------------------|------------------------|
| Direct Digital     | Simple design             | Less flexible          |
| Impulse Invariance | Preserves impulse response| Aliasing possible      |
| Bilinear Transform | No aliasing, accurate     | Frequency warping      |

---

# Conclusion
- All three methods successfully design low-pass Butterworth filters.  
- Bilinear transformation is generally preferred due to no aliasing.  
- MATLAB tools simplify filter design and analysis.
