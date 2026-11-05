# ARTI403 / ARTI404 – Image Processing: Lab 9 (Morphological Image Processing)

## Overview

This repository contains the implementation and results for **Lab 9: Morphological Image Processing**. The lab explores how various morphological operations; including erosion, dilation, opening, and closing; extract and modify structural shapes in binary images, and investigates the impact of adjusting structuring element shapes and sizes.

## Tools & Libraries Used

- Language: Python 3
- Environment: Jupyter Notebook
- Libraries: OpenCV (cv2), NumPy, Matplotlib

## Tasks Implemented

### 1. Apply Morphological Operations to a New Image

- Loaded a binary image (`Balls.png`) using Otsu's thresholding.
- Applied the core morphological operations: Erosion, Dilation, Opening, and Closing.
- Displayed the original binary image alongside the results of each operation for visual comparison.

### 2. Experiment with Structuring Elements

- Applied erosion and dilation using three different structuring element shapes: Square, Cross, and Ellipse (`cv2.MORPH_RECT`, `cv2.MORPH_CROSS`, `cv2.MORPH_ELLIPSE`).
- Experimented across multiple kernel sizes ($3\times3$, $5\times5$, and $7\times7$).
- Compared the resulting images side by side to evaluate how kernel shape and size configuration affect foreground objects.

## What I Learned

1. **Operation Effects:** Erosion shrinks or removes foreground pixels and eliminates small isolated noise, whereas dilation expands foreground boundaries, filling small holes. Opening (erosion followed by dilation) removes small noise spots without significantly changing object sizes, and closing (dilation followed by erosion) bridges small gaps and smooths out boundaries.
2. **Impact of Structuring Element Shapes:** The geometric shape of the kernel directly influences how edges and corners react during transformations. For instance, rectangular and elliptical kernels expand or shrink regions uniformly across directions, whereas cross-shaped kernels preserve diagonal structures differently.
3. **Scale Dependency of Kernel Sizes:** Increasing the kernel size from $3\times3$ to $7\times7$ magnifies the effect of erosion and dilation, leading to heavier erosion of thin features or broader dilation coverage, which requires careful tuning based on target object dimensions.

## Repository Structure

```text
Lab9/
├── Lab 9_Morphological_Operations.ipynb            # Jupyter Notebook implementing Lab 9 techniques of the tasks
├── Solution.ipynb                                  # Jupyter Notebook implementing Lab 9 tasks
├── Lab9.pdf                                        # Exported PDF version of the notebook
├── Balls.png                                       # Provided sample binary image used for experiments
├── BoundaryExtraction.png                          # Provided sample binary image used for experiments
├── Erosion.png                                     # Provided sample binary image used for experiments
├── Erosion2.png                                    # Provided sample binary image used for experiments
├── Opening2.png                                    # Provided sample binary image used for experiments
├── Open_Closing.png                                # Provided sample binary image used for experiments
└── README.md                                       # Lab documentation and key takeaways
