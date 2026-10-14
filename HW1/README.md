# HW1: Image Processing & Discrete-Time Signals

Practical assignment covering change-of-basis methods for images and fundamentals of discrete-time systems.

## Contents

### Q1: Image Compression & Denoising (SVD vs. FFT)
- **Compression:** A grayscale image is compressed at rates of 0.1%, 0.5%, 1%, 5% and 10% using truncated SVD and 2D-FFT coefficient selection, and the two methods are compared visually.
- **Denoising:** A noisy image is denoised with low-rank SVD approximation (multiple ranks tested) and with FFT low-pass filtering (multiple cutoff radii tested), finding the best threshold empirically.
- **Finding:** SVD generally performs better, since its bases adapt to the image content, while FFT relies on fixed sinusoidal bases.

### Q2: Z-Transform Analysis
For the system `y[n] - 0.5y[n-1] + 0.25y[n-2] = x[n] + 2x[n-1] + x[n-3]`:
- Impulse response computed recursively and via the Z-transform
- Pole-zero analysis and stability check (all poles inside the unit circle, so the system is stable)
- Response to a multi-tone input
- Magnitude and phase frequency responses

### Q3: Low-Pass & High-Pass Filter Design
- Design of a first-order low-pass filter with cutoff ω_c = 0.3π and its high-pass counterpart
- Frequency responses, filtering of a test signal, and pole-zero plots for both filters

## Files

| File | Description |
|---|---|
| `HW1.ipynb` | Full solution notebook |
| `images/` | Input images (original image, noisy image) |
| `samples/` | Reference figures embedded in the notebook: a 2D-FFT diagram and example outputs for compression, SVD denoising and FFT denoising |

> Note: image paths in the notebook point to `/content/images` (Google Colab). Change them to `./images` to run locally.
