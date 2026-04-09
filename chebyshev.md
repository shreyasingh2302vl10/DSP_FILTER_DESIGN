# Chebyshev Type-I Low Pass Digital Filter Design (MATLAB)

This README contains MATLAB implementations for **Chebyshev Type-I low-pass digital filter design** using three methods:

* Direct Digital Design
* Impulse Invariance Technique
* Bilinear Transformation Technique

---

## Direct Low Pass Chebyshev-I Filter Design

### Specifications

* Passband cutoff: `Ωp = 0.2π`
* Stopband cutoff: `Ωs = 0.3π`
* Passband ripple: `Rp = 1 dB`
* Stopband attenuation: `As = 16 dB`

### MATLAB Code

```matlab
clc;
clear;
close all;

wp = 0.2;
ws = 0.3;
Rp = 1;
As = 16;

[N, Wn] = cheb1ord(wp, ws, Rp, As);
[b, a] = cheby1(N, Rp, Wn, 'low');

disp(['Filter Order N = ', num2str(N)]);
disp(['Cutoff Frequency Wn = ', num2str(Wn)]);

freqz(b, a, 1024);
title('Chebyshev Type-I Low Pass Filter');
```

### Result

The direct digital Chebyshev-I low pass filter is designed and its frequency response is verified using `freqz()`.

---

##  Low Pass Chebyshev-I using Impulse Invariance

### Specifications

* Passband frequency: `ωp = 0.2π`
* Stopband frequency: `ωs = 0.3π`
* Passband ripple: `Rp = 1 dB`
* Stopband attenuation: `As = 15 dB`

### MATLAB Code

```matlab
clc;
clear;
close all;

wp = 0.2 * pi;
ws = 0.3 * pi;
Rp = 1;
As = 15;
T = 1;

Omega_p = wp / T;
Omega_s = ws / T;

[N, Omega_p_new] = cheb1ord(Omega_p, Omega_s, Rp, As, 's');
[b, a] = cheby1(N, Rp, Omega_p_new, 's');

[bd, ad] = impinvar(b, a, 1/T);

disp(['Filter Order N = ', num2str(N)]);
disp(['Adjusted Passband Frequency = ', num2str(Omega_p_new)]);

freqz(bd, ad, 1024);
title('Chebyshev-I using Impulse Invariance');
```

### Result

The analog Chebyshev-I filter is converted into digital form using the **impulse invariance method**.

---

## Low Pass Chebyshev-I using Bilinear Transformation

### Specifications

* Passband frequency: `ωp = 0.2π`
* Stopband frequency: `ωs = 0.3π`
* Passband ripple: `Rp = 1 dB`
* Stopband attenuation: `As = 15 dB`

### MATLAB Code

```matlab
clc;
clear;
close all;

wp = 0.2 * pi;
ws = 0.3 * pi;
Rp = 1;
As = 15;
T = 1;

Omega_p = (2/T) * tan(wp/2);
Omega_s = (2/T) * tan(ws/2);

[N, Omega_p_new] = cheb1ord(Omega_p, Omega_s, Rp, As, 's');
[b, a] = cheby1(N, Rp, Omega_p_new, 's');

[bd, ad] = bilinear(b, a, 1/T);

disp(['Filter Order N = ', num2str(N)]);
disp(['Adjusted Passband Frequency = ', num2str(Omega_p_new)]);

freqz(bd, ad, 1024);
title('Chebyshev-I using Bilinear Transformation');
```

### Result

The analog filter is transformed into digital form using the **bilinear transformation method**, which avoids aliasing.

---

## Conclusion

The **Chebyshev Type-I low pass filter** was successfully designed using:

1. Direct digital design
2. Impulse invariance
3. Bilinear transformation

Among these, **bilinear transformation is the most practical method** because it avoids aliasing and preserves filter characteristics effectively.
