# ARTI403 / ARTI404 – Image Processing: Lab 8 (Edge Detection)

## Overview

This repository contains the implementation and results for **Lab 8: Edge Detection**. The lab explores how various edge detection algorithms extract structural information from images and investigates the impact of adjusting algorithm parameters, specifically Canny thresholds.

## Tools & Libraries Used

- Language: Python 3
- Environment: Jupyter Notebook
- Libraries: OpenCV (cv2), NumPy, Matplotlib

## Tasks Implemented

### 1. Apply Edge Detection Methods

- Loaded a custom image and applied Gaussian blur to reduce noise prior to edge detection.
- Computed and compared edge maps using Sobel, Prewitt, and Canny edge detectors.
- Displayed the original image alongside the three distinct edge maps for visual comparison.

### 2. Investigate the Effect of Canny Thresholds

- Applied the Canny edge detector using three different threshold pairs: Low= 30/High= 90, Low= 50/High= 150, and Low= 100/High= 200.
- Displayed the resulting edge maps side by side to evaluate how threshold changes affect the output.
- Overlaid the detected 1-channel Canny edges back onto the 3-channel RGB image for colorized edge enhancement.

## What I Learned

1. **Algorithm Differences:** Sobel and Prewitt filters are gradient-based and compute the first-order derivatives to find edges, which can sometimes result in thicker edges. The Canny edge detector is a multi-stage algorithm that generally provides thinner, cleaner, and more continuous edges.
2. **Impact of Thresholding:** In the Canny algorithm, lowering the hysteresis thresholds (e.g., 30/90) detects more subtle edges but introduces noise, whereas increasing them (e.g., 100/200) filters out weak gradients and isolates only the most prominent structural boundaries.
3. **Management of the Channel in OpenCV:** NumPy boolean array indexing requires matching dimensions. To overlay a 1-channel grayscale edge map onto a 3-channel RGB image, the background must first be converted or mapped properly (e.g., converting 1-channel to 3-channel with cv2.cvtColor or creating a np.zeros_like array) to avoid assignment errors.

## Repository Structure

```text
Lab8/
├── Lab_8_Edge_Detection.ipynb  # Edge Detection outputs
├── Solution.ipynb              # Tasks
├── Lab8.pdf                    # Exported PDF version of the notebook
├── kid1.jpg                    # Provided sample image
├── Coins.jpg                   # Provided sample image
├── bird.jpg                    # Provided sample image
├── Butterfly.jpg               # Provided sample image
├── Mercedes Automobile.png     # Custom input image used for Task 1 and Task 2
└── README.md                   # Lab documentation and key takeaways
```
