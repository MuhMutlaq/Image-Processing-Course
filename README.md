# ARTI403 / ARTI404 – Image Processing: Lab 7 (Spatial Domain Filtering)

## Overview

This repository contains the implementation and results for **Lab 7: Spatial Domain Filtering**. The lab is divided into two main sections: **Lab 7(A) - Laplacian Filter** and **Lab 7(B) - Mathematical and Statistical Filters**. It explores how spatial filters can be utilized directly on image pixels to achieve image sharpening and effective noise reduction.

## Tools & Libraries Used

- **Language:** Python 3
- **Environment:** Jupyter Notebook
- **Libraries:** `OpenCV` (`cv2`), `NumPy`, `IPython.display`, `Matplotlib`

## Tasks Implemented

### 1. Lab 7(A): Laplacian Filter (Image Sharpening)

- Loaded the input image to prepare it for spatial processing.
- Applied the Laplacian operator to compute the second-order spatial derivatives, capturing areas of rapid intensity change.
- Processed the image to achieve a sharpening effect, enhancing fine details and edges to produce a crisp output.

### 2. Lab 7(B): Mathematical and Statistical Filters (Noise Reduction)

- Loaded various images corrupted with different types of noise artifacts, specifically utilizing the provided samples (`noise.jpg`, `salt&Pepper.jpg`, and `salt&Pepper2.jpg`).
- Applied mathematical (Mean/Box) filters to evaluate their effect on general image noise.
- Applied statistical (Median) filters to target and eliminate impulse noise (salt-and-pepper noise) while evaluating edge preservation.

## What I Learned

1. **Second-Order Derivatives for Sharpening:** The Laplacian filter acts as an isotropic measure of the 2D spatial derivative of an image. By combining the Laplacian result with the original image, you can effectively enhance fine details and sharpen blurry images (like the standard moon example).
2. **Linear vs. Non-Linear Filtering:** Mathematical filters (like the Mean filter) operate linearly by averaging local pixel values, which smooths out Gaussian noise but noticeably blurs sharp edges. In contrast, statistical filters (like the Median filter) are non-linear and replace the center pixel with the median of its neighborhood.
3. **Handling Impulse Noise:** The Median filter is vastly superior to the Mean filter when dealing with salt-and-pepper noise. It completely removes the extreme black and white pixel spikes without severely degrading the underlying edges of the subjects.

## Repository Structure

```text
Lab7/
├── Solution.ipynb             # Complete Jupyter Notebook with code and outputs
├── Lab7.pdf                   # Exported PDF version of the notebook
├── images/
├── moon.jpg                   # Unsharpened input image for Lab 7(A)
├── noise.jpg                  # Input image with general noise for Lab 7(B)
├── salt&Pepper.jpg            # Input image with salt and pepper noise
├── salt&Pepper2.jpg           # Additional input image with salt and pepper noise
└── README.md                  # Lab documentation and key takeaways
```
