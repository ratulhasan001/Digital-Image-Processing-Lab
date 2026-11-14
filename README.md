# digital-image-processing-lab

Jupyter notebooks from the Digital Image Processing sessional (lab) course of the B.Sc. in Computer Science and Engineering at BAUET. Most operations are written by hand with NumPy loops instead of library calls: spatial filtering, unsharp masking, morphological erosion and dilation, gradient and Laplacian edge detectors, and a step-by-step Canny edge detector. Where OpenCV has an equivalent (for example `cv2.erode`), the notebook runs it as well so the two results can be compared.

## Contents

| Notebook | What it does |
|---|---|
| [Filtering.ipynb](Filtering.ipynb) | Spatial filtering with a user-entered `x × y` kernel. Slides the kernel over a grayscale image and takes the mean of each neighbourhood multiplied element-wise by the kernel. A comment notes that the same loop gives min, median or max filters. O(M·N·x·y). |
| [Image%20Sharpening.ipynb](Image%20Sharpening.ipynb) | Unsharp masking. Smooths the image with the averaging filter above, computes the mask `image − smoothed`, then forms `image + k·mask` for a user-entered `k`. |
| [Erosion.ipynb](Erosion.ipynb) | Binary erosion written by hand. Otsu thresholding, then the minimum over each neighbourhood under a user-entered structuring element. Shown next to `cv2.erode` for comparison. |
| [Dilation.ipynb](Dilation.ipynb) | Binary dilation written by hand: the maximum over each neighbourhood. It reuses the erosion notebook's code, so the helper function is still named `erosion`. Note that the built-in reference plot still calls `cv2.erode`, not `cv2.dilate`, so the two images it shows are different operations. |
| [Different%20Edge%20Detection.ipynb](Different%20Edge%20Detection.ipynb) | Applies edge kernels with `cv2.filter2D`: horizontal and vertical line detectors, Roberts cross, Prewitt, Sobel (gradient magnitude √(Gx² + Gy²)), and Laplacian with 4- and 8-neighbour kernels. |
| [Canny%20Edge%20Detection.ipynb](Canny%20Edge%20Detection.ipynb) | Canny edge detection written by hand: Gaussian blur → Sobel gradients (magnitude and direction) → non-maximum suppression over 4 quantised directions → double threshold and hysteresis (low 20, high 40). |

## Requirements

The notebooks were written with Python 3.12 (Anaconda) and use:

- `opencv-python` (`cv2`)
- `numpy`
- `matplotlib`

```bash
pip install notebook opencv-python numpy matplotlib
jupyter notebook
```

## Running the notebooks

- **Test images are not included.** Each notebook loads its image from a hard-coded relative path:
  - `Downloads/img.jpg` in Filtering, Image Sharpening, Erosion and Dilation.
  - `Downloads/clock.jpg` in Different Edge Detection.
  - `downlaods/img.jpg` in Canny Edge Detection.

  Before running, change the `cv2.imread(...)` path to an image on your machine.
- **Kernel input.** Filtering, Image Sharpening, Erosion and Dilation read the kernel from standard input. First enter its size `x y`, then `x` rows of `y` integers. For example, `3 3` followed by three rows of `1 1 1` gives a 3 × 3 averaging kernel or a square structuring element. Image Sharpening then asks for the sharpening factor `k`.
- **No saved outputs.** The notebooks are stored without outputs, so run them to see the figures.

## Author

Ratul Hasan · [ratulhasan.dev](https://ratulhasan.dev)
