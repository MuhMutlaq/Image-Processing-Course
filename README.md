# Digital Image Processing Lab: Sampling, Quantization & Image Arithmetic / Set Operations

This repository documents the practical implementations, mathematical principles, and key takeaways learned during this Digital Image Processing lab session.

## Student Information

**Name:** Muhannad Almutlaq
**ID:** 2240006060

---

## Table of Contents

- [Digital Image Processing Lab: Sampling, Quantization \& Image Arithmetic / Set Operations](#digital-image-processing-lab-sampling-quantization--image-arithmetic--set-operations)
  - [Student Information](#student-information)
  - [Table of Contents](#table-of-contents)
  - [Lab Overview](#lab-overview)
  - [Core Topics \& Key Learnings](#core-topics--key-learnings)
    - [1. Spatial Sampling (Downsampling \& Resolution)](#1-spatial-sampling-downsampling--resolution)
    - [2. Gray-Level Quantization](#2-gray-level-quantization)
    - [3. Arithmetic Operations \& Saturation Handling](#3-arithmetic-operations--saturation-handling)
    - [4. Set Theory \& Fuzzy Operations on Grayscale Images](#4-set-theory--fuzzy-operations-on-grayscale-images)
  - [Lab Tasks \& Implementation Details](#lab-tasks--implementation-details)
    - [Initial Experiments: Image Blending \& Union](#initial-experiments-image-blending--union)
    - [Task 1: Sampling \& Quantization Parameter Variations](#task-1-sampling--quantization-parameter-variations)
    - [Task 2: Image Arithmetic \& Gray-Scale Set Operations](#task-2-image-arithmetic--gray-scale-set-operations)
      - [1. Image Subtraction](#1-image-subtraction)
      - [2. Brightness Adjustment (Constant Addition)](#2-brightness-adjustment-constant-addition)
      - [3. Set Difference ($X \\setminus Y$)](#3-set-difference-x-setminus-y)
      - [4. Symmetric Difference ($X \\Delta Y$)](#4-symmetric-difference-x-delta-y)
      - [5. Set Intersection ($X \\cap Y$)](#5-set-intersection-x-cap-y)
  - [Tools \& Libraries](#tools--libraries)
  - [Summary of Key Takeaways](#summary-of-key-takeaways)

---

## Lab Overview

The primary objective of this lab was to explore fundamental digital image processing concepts at the pixel and array levels:

- Converting continuous/high-resolution image spaces into discrete spatial domains (**sampling**) and discrete amplitude domains (**quantization**).
- Overcoming integer overflow/underflow hazards in byte-based arithmetic.
- Applying set-theoretic and fuzzy-logic operators (Union, Intersection, Complement, Set Difference, and Symmetric Difference) to multi-level grayscale imagery.

---

## Core Topics & Key Learnings

### 1. Spatial Sampling (Downsampling & Resolution)

- **Concept:** Sampling determines the spatial resolution of a digital image ($M \times N$ grid of pixels).
- **Subsampling/Downsampling:** Reduces the pixel density by an integer factor or scaling factor ($f < 1$).
- **Visual Artifacts:**
  - Aggressive downsampling removes high-frequency spatial details (edges, fine textures).
  - Restoring a downsampled image back to original dimensions using Nearest-Neighbor interpolation produces noticeable pixelation, jagged edges, and checkerboard blocking.

### 2. Gray-Level Quantization

- **Concept:** Quantization determines the intensity resolution (number of discrete brightness levels, $L = 2^k$ for $k$ bits). Standard grayscale utilizes 8 bits ($L = 256$, $[0, 255]$).
- **Bit-Depth Reduction:** Reducing $k$ clusters continuous tone gradients into coarse bins:
  $$\text{Quantized}(x, y) = \left\lfloor \frac{I(x, y)}{256 / L} \right\rfloor \times \left( \frac{255}{L - 1} \right)$$
- **Visual Artifacts:**
  - When $k \le 3$ (8 levels or fewer), continuous gradients degrade into distinct steps/bands—an artifact known as **false contouring** or banding.

### 3. Arithmetic Operations & Saturation Handling

- **Data Type Hazards:** Grayscale images are natively represented as unsigned 8-bit integers (`uint8`, range $0$ to $255$).
  - Simple addition (`200 + 100 = 300`) will roll over (`300 % 256 = 44`), creating inverted dark patches.
  - Subtraction (`50 - 100 = -50`) will wrap around to $206$ in standard unsigned arithmetic.
- **Solution Learned:**
  - Cast arrays to wider numerical types (`uint16` or `int32`/`float32`) prior to arithmetic.
  - Apply saturation clamping: `np.clip(result, 0, 255).astype(np.uint8)` or compute absolute difference `np.abs(A - B)`.

### 4. Set Theory & Fuzzy Operations on Grayscale Images

Unlike binary images (where sets are simple $0$ or $1$ masks), grayscale pixel values $[0, 255]$ are treated as fuzzy set membership functions scaled by $255$:

- **Complement ($A^c$):** $255 - A$
- **Intersection ($A \cap B$):** Pointwise minimum $\min(A, B)$ (or bitwise AND `A & B` for thresholded/binary sets).
- **Union ($A \cup B$):** Pointwise maximum $\max(A, B)$ (or bitwise OR `A | B`).
- **Set Difference ($A \setminus B$):** $A \cap B^c = \min(A, 255 - B)$ or non-negative bounded subtraction $\max(A - B, 0)$.
- **Symmetric Difference ($A \Delta B$):** $(A \setminus B) \cup (B \setminus A) = \max(\min(A, 255 - B), \min(B, 255 - A))$ or pointwise $|A - B|$.

---

## Lab Tasks & Implementation Details

### Initial Experiments: Image Blending & Union

1. **Linear Addition with Clamping:**
   - Resized both images to uniform dimensions ($400 \times 400$) using Lanczos resampling.
   - Upcasted to `np.uint16`, added pixel intensities, and saturated via `np.clip(..., 0, 255)`.
2. **Bitwise Union:**
   - Applied `im4arr | im3arr` to evaluate bitwise OR overlay effects.

---

### Task 1: Sampling & Quantization Parameter Variations

Implemented a modular sampling and quantization pipeline:

```python
def sample_and_quantize(image_path, scale_factor= 0.25, bits= 2):
    img= Image.open(image_path).convert('L')
    orig_w, orig_h= img.size
    
    # 1. Spatial Downsampling & Restoration
    new_w, new_h= max(1, int(orig_w * scale_factor)), max(1, int(orig_h * scale_factor))
    sampled_img= img.resize((new_w, new_h), Image.Resampling.NEAREST)
    sampled_restored= sampled_img.resize((orig_w, orig_h), Image.Resampling.NEAREST)
    
    # 2. Intensity Quantization (L = 2^bits levels)
    levels= 2 ** bits
    arr= np.asarray(sampled_restored, dtype=np.float32)
    quantized_arr= np.floor(arr / (256.0 / levels)) * (255.0 / (levels - 1))
    quantized_img= Image.fromarray(quantized_arr.astype(np.uint8))
    
    return quantized_img
```

- **Observations:**
  - High sampling factors (e.g., $14$) substantially coarsen image edges.
  - Low bit-depths ($k=2$ or $4$ gray levels) make complex scenes look posterized with sharp pseudo-edges.

---

### Task 2: Image Arithmetic & Gray-Scale Set Operations

#### 1. Image Subtraction

- **Formula:** $|X - Y|$
- **Code:**

    ```python
    subtraction= np.abs(X - Y).astype(np.uint8)
    ```

- **Application:** Highlights motion, changes between frames, or high-contrast structural differences.

#### 2. Brightness Adjustment (Constant Addition)

- **Formula:** $\text{clamp}(X + 175, 0, 255)$
- **Code:**

    ```python
    addition_const= np.clip(X + 175, 0, 255).astype(np.uint8)
    ```

- **Application:** Uniform brightening with clipping at maximum white saturation ($255$).

#### 3. Set Difference ($X \setminus Y$)

- **Formula:** $\min(X, 255 - Y)$
- **Code:**

    ```python
    complement_Y= 255 - Y
    set_difference= np.minimum(X, complement_Y).astype(np.uint8)
    ```

- **Result:** Retains features that are prominent in $X$ while suppressing regions where $Y$ is bright.

#### 4. Symmetric Difference ($X \Delta Y$)

- **Formula:** $\max(\min(X, 255 - Y), \min(Y, 255 - X))$
- **Code:**

    ```python
    diff_X_Y= np.minimum(X, 255 - Y)
    diff_Y_X= np.minimum(Y, 255 - X)
    symmetric_difference= np.maximum(diff_X_Y, diff_Y_X).astype(np.uint8)
    ```

- **Result:** Extracts non-overlapping intensity features between both images.

#### 5. Set Intersection ($X \cap Y$)

- **Formula:** $\min(X, Y)$
- **Code:**

    ```python
    intersection= np.minimum(X, Y).astype(np.uint8)
    ```

- **Result:** Keeps the darker common baseline intensity between both images.

---

## Tools & Libraries

| Library | Role in Lab |
| :--- | :--- |
| **NumPy (`numpy`)** | Multi-dimensional array manipulations, vectorized operations, type-casting (`uint16`, `int32`), arithmetic clamping (`clip`, `minimum`, `maximum`, `abs`). |
| **Pillow (`PIL.Image`)** | Image loading, conversion to grayscale (`'L'`), resampling/resizing (`LANCZOS`, `NEAREST`), and display. |
| **OpenCV (`cv2`)** | Grayscale reading (`IMREAD_GRAYSCALE`), fast spatial resizing (`INTER_NEAREST`). |
| **Matplotlib (`plt`)** | Subplot visualization comparing original, sampled, and quantized images side-by-side. |

---

## Summary of Key Takeaways

1. **Resolution Dependencies:** Spatial resolution depends on sampling rate, while contrast fidelity depends on quantization depth. Both must be balanced to minimize bandwidth without causing checkerboarding or false contouring.
2. **Safe Array Computing:** Grayscale digital image arithmetic in Python requires explicit precision management (`int32` / `float32`) and saturation clipping to avoid modulo wrapping.
3. **Fuzzy vs. Bitwise Sets:** Set operations on grayscale images are rigorously defined using Zadeh's min/max fuzzy logic, differing fundamentally from simple binary masking.
