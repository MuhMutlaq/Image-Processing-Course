# ARTI 404 – Image Processing: Lab 4

**Session Topic:** Intensity Transformations and Filtering-Spatial Domain  
**Academic Year:** 2025 - 2026

## Objective

The primary outcome of this lab is to write a program that implements fundamental image processing algorithms, specifically focusing on image thresholding and histogram processing techniques.

## Tools and Technologies

* **Language:** Python 3
* **Environment:** Anaconda / Jupyter Notebook
* **Libraries Used:** OpenCV, NumPy, Matplotlib, Scikit-Image (Skimage)

## Repository Structure

Ensure the `Lab#4` folder contains the following structure before running the notebook:

```text
├── Lab4.ipynb                 # The main Jupyter Notebook containing all tasks
├── images/                    # Directory for input images
│   ├── Parrot.png
│   └── (Additional skimage.data images are downloaded automatically)
├── outputs/                   # Directory for saved threshold outputs
└── Lab4.pdf            # PDF version of the report for Blackboard submission
```

## What I Learned

* **Image Segmentation via Thresholding:** Segmented images into foreground and background by applying fixed threshold values using OpenCV, demonstrating how varying the threshold directly impacts binary image generation.

* **Contrast Stretching:** Improved image visibility by rescaling pixel intensities to span a wider dynamic range, specifically targeting percentile bounds (e.g., 3rd to 80th) to ignore extreme dark or light pixel outliers.

* **Histogram Equalization:** Enhanced global image contrast automatically by utilizing `skimage` to flatten the image histogram, distributing intensity values evenly across the available spectrum.

* **Histogram Matching:** Transferred the color and contrast characteristics of a reference image (Rocket) to a source image (Chelsea) by aligning their histograms across all RGB color channels.

* **Analytical Visualization:** Utilized Matplotlib subplots to effectively map and compare spatial domain outputs side-by-side with their corresponding statistical histograms.
