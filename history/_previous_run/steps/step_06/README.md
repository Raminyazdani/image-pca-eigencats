# Image PCA and Eigenface Analysis

**Principal Component Analysis on image data with dimensionality reduction**

**Stack:** Python, NumPy, Matplotlib, Jupyter Notebook

## Overview

This project demonstrates Principal Component Analysis (PCA) applied to facial images, computing "eigencats" - principal components that represent the most significant variations in a cat face dataset. It showcases dimensionality reduction, eigendecomposition, and image reconstruction using linear algebra techniques fundamental to computer vision and machine learning.

## Problem & Approach

**Problem:** Apply PCA to a dataset of cat face images to extract principal components and enable efficient image representation and reconstruction.

**Approach:**
- Load and preprocess 64x64 grayscale cat face images
- Compute mean cat face and center the data
- Perform eigendecomposition to find principal components (eigencats)
- Visualize eigencats and their contribution to variance
- Reconstruct original images using linear combinations of eigencats
- Demonstrate dimensionality reduction by using fewer components

## Tech Stack

- **Python 3.6+** - Core programming language
- **NumPy** - Linear algebra operations and eigendecomposition
- **Matplotlib** - Visualization of eigencats and reconstructions
- **Jupyter Notebook** - Interactive analysis environment

## Folder Structure

```
image-pca-eigencats/
├── eigencats.ipynb       # PCA implementation and analysis
├── cats.npy              # Cat image dataset (64x64 grayscale)
├── imgs/                 # Reference visualizations
│   ├── eigencats.png     # Eigencat components visualization
│   └── meancat.png       # Mean cat face visualization
├── requirements.txt      # Python dependencies
└── README.md             # This file
```

## Setup / Installation

1. **Ensure Python 3.6+ is installed**

2. **Install dependencies:**
```bash
pip install -r requirements.txt
```

Or manually:
```bash
pip install numpy matplotlib jupyter
```

## How to Run

1. **Navigate to project directory:**
```bash
cd /path/to/image-pca-eigencats
# Or work from the repository root
```

2. **Launch Jupyter Notebook:**
```bash
jupyter notebook eigencats.ipynb
```

3. **Execute cells sequentially** from top to bottom

Alternative with JupyterLab:
```bash
jupyter lab eigencats.ipynb
```

## Data / Inputs

**Input Files:**
- `cats.npy` - NumPy binary array containing preprocessed 64×64 grayscale cat face images
- `imgs/eigencats.png` - Reference visualization of computed eigencats
- `imgs/meancat.png` - Reference visualization of mean cat face

**Data Format:**
- NumPy array shape: (n_images, 64, 64)
- Grayscale pixel values (typically normalized 0-255 or 0-1)

**Data Location:** All files in project directory with reference images in `imgs/` subdirectory

## Outputs

**Computed Results:**
- Mean cat face (average across all images)
- Eigencats (principal components ordered by variance)
- Eigenvalues representing variance explained by each component
- Reconstructed cat faces from selected eigencats

**Visualizations:**
- Grid of top eigencats showing facial variation patterns
- Reconstruction quality comparison with varying numbers of components
- Cumulative variance explained plots

## Reproducibility Notes

- All computations are deterministic (no randomness)
- Eigendecomposition results may vary slightly with different NumPy/BLAS versions
- All file paths are relative to project directory
- Notebook includes `plot_cats()` helper function for consistent visualization
- No external data download required - dataset included

## Troubleshooting

**Common Issues:**

- **Import errors:** Install dependencies with `pip install numpy matplotlib jupyter`
- **File not found:** Ensure `cats.npy` is in the same directory as notebook
- **Python version:** Requires Python 3.6+ for type hints
- **Missing images:** Verify `imgs/` directory exists with reference images
- **Display issues:** 
  - Try `%matplotlib inline` magic command
  - Restart kernel if images don't render

**Performance:**
- Large datasets may require significant memory for covariance computation
- Consider using incremental PCA for very large image sets

## Notes

- Originally created in an academic setting
- Demonstrates fundamental linear algebra concepts in computer vision
- "Eigenfaces" technique (here "eigencats") developed in early face recognition research
- Principal components capture major facial variations (position, lighting, expression)
- Technique applicable to any high-dimensional data (faces, documents, signals)
- First few eigencats typically capture most variance (efficient representation)
