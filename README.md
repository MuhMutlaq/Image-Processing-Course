# ARTI403 / ARTI404 – Image Processing: Lab 6 (Frequency Domain)

## Overview

This repository contains the implementation and assessment solutions for **Lab 6: Filtering in the Frequency Domain**. The lab explores how spatial derivative operators (Laplacian and Sobel edge detectors) can be formulated and applied in the frequency domain using the 2D Fast Fourier Transform (FFT) and the Convolution Theorem.

---

## Tools & Libraries Used

* **Language:** Python 3
* **Environment:** Jupyter Notebook
* **Libraries:** `NumPy`, `scikit-image` (`skimage`), `Matplotlib`

---

## Tasks Implemented

### 1. Procedural Task: Laplacian Filter in the Frequency Domain

* Loaded and resized the standard grayscale `camera` image to $256 \times 256$.
* Constructed a 2D frequency grid using `np.fft.fftfreq`.
* Formulated the analytical frequency-domain Laplacian transfer function:
  $$H(u, v)= -4\pi^2(u^2 + v^2)$$
* Multiplied the 2D FFT of the image $F(u,v)$ by $H(u,v)$ and reconstructed the edge-enhanced spatial image using the Inverse 2D FFT (`ifft2`).

### 2. Assessment Task: Sobel Filters in the Frequency Domain

* Defined the $3 \times 3$ spatial Sobel kernels ($G_x$ for vertical edges and $G_y$ for horizontal edges).
* Implemented `center_embed_kernel(kernel, shape)` to zero-pad the $3 \times 3$ kernels to match the $256 \times 256$ image size and center them.
* Applied `ifftshift` prior to `fft2` to align the center of the spatial kernel with the $(0, 0)$ origin of the array, preventing spatial phase shifts in the reconstructed output.
* Performed point-wise multiplication in the frequency domain ($F \cdot H_x$ and $F \cdot H_y$), transformed the results back to the spatial domain via `ifft2`, and computed the overall gradient magnitude:
  $$\vert{}G\vert{}= \sqrt{G_x^2 + G_y^2}$$

---

## What I Learned

1. **The Convolution Theorem in Practice:** Convolving an image with a spatial filter kernel $h(x, y)$ is mathematically equivalent to point-wise multiplication of their Fourier transforms $F(u, v) \cdot H(u, v)$ in the frequency domain.
2. **High-Pass Nature of Derivative Filters:** Both Laplacian and Sobel operators act as high-pass filters in the frequency domain—they attenuate low-frequency components (smooth, homogeneous background regions) and amplify high-frequency components (sharp intensity transitions and edges).
3. **Isotropic vs. Directional Filtering:** The Laplacian filter is isotropic (rotationally invariant), capturing edges in all directions simultaneously, whereas Sobel filters are directional, isolating vertical ($G_x$) and horizontal ($G_y$) frequency components separately before combining them.
4. **Zero-Padding and Zero-Phase Alignment (`ifftshift`):** When converting a small spatial kernel (like a $3 \times 3$ Sobel filter) to the frequency domain, the kernel must be zero-padded to the target image dimensions. Furthermore, centering the kernel and applying `ifftshift` before taking the FFT ensures the kernel's origin is positioned at $(0, 0)$, eliminating circular shift distortion in the final spatial image.

---

## Repository Structure

```text
Lab6/
├── Solution.ipynb                   # Complete Jupyter Notebook with code and outputs
├── Lab6.pdf                         # Exported PDF version of the notebook
├── images/
│   ├── cameraman.png                # Input image used in the lab
│   ├── task1_laplacian_results.png  # Output plot for Procedural Task #1
│   └── assessment_sobel_results.png # Output plot for Assessment Task #1
└── README.md                        # Lab documentation and key takeaways
```

---

## How to Run

1. Clone this repository and navigate to the `Lab6` folder.
2. Install the required dependencies:

    ```bash
    pip install numpy matplotlib scikit-image jupyter
    ```

3. Launch Jupyter Notebook and run all cells:

    ```bash
    jupyter notebook Solution.ipynb
    ```
