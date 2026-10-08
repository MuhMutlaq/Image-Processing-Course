# Lab 5: Spatial Filtering – Smoothing and Sharpening

**Course:** ARTI 406 – Image Processing  
**Institution:** Imam Abdulrahman Bin Faisal University, College of Computer Science and Information Technology

## Overview

This repository contains the Jupyter Notebook and source images for Lab 5. The primary objective of this session was to write programs that implement fundamental image processing algorithms, focusing specifically on spatial filtering techniques for smoothing (blurring) and sharpening images.

## Tools & Environment

* **Language:** Python 3
* **Environment:** Anaconda / Jupyter Notebook
* **Key Libraries:** OpenCV, NumPy, Pillow, Skimage, Matplotlib

## What I Did (Lab Tasks)

* **Unsharp Masking:** Implemented an unsharp masking technique by applying a Gaussian blur and blending it back with the original float32 image to enhance sharpness.
* **Box Filtering:** Convolved an image with a 7x7 box filter (`cv2.blur`) to observe basic averaging and smoothing, outputting the results side-by-side.
* **Gaussian Filtering:** Applied both a 5x5 and a 21x21 Gaussian filter (`cv2.GaussianBlur`) to compare the varying intensities of blur.
* **Laplacian Sharpening:** Applied a 3x3 Laplacian filter (`cv2.Laplacian`) to detect edges and sharpen the image. I subtracted the Laplacian output from the original image and clipped the values between 0 and 1 using `np.clip`.

## What I Learned

* **Kernel Convolution:** Gained hands-on experience applying different convolutional filters (Box, Gaussian, Laplacian) directly to image matrices to manipulate visual data.
* **Data Type Handling:** Learned the importance of converting standard 8-bit images to `float32` arrays divided by 255.0. This maintains precision when performing mathematical operations on pixels, such as the subtraction required for Laplacian sharpening.
* **Debugging Matplotlib Visualizations:** Discovered how Matplotlib handles floating-point image arrays. I learned how to properly map negative gradients (produced by the Laplacian second-derivative filter) to valid `[0.0, 1.0]` ranges using absolute values and clipping. This resolved issues with Matplotlib throwing range warnings and displaying harsh black-and-white visual artifacts or flattened gray images.
