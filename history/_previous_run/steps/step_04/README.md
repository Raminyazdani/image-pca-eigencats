# Image PCA & Eigencats Analysis

Principal Component Analysis on cat face images.

## Overview

Demonstrates PCA applied to cat faces to extract eigencats - principal components representing facial variations.

## Tech Stack

- Python 3.6+, NumPy, Matplotlib, Jupyter Notebook

## Setup

```bash
pip install -r requirements.txt
```

## Run

```bash
jupyter notebook eigencats.ipynb
```

## Data

- `cats.npy` - 80 cat face images (64x64 grayscale)
- `imgs/` - Reference visualizations

## Features

- Preprocessing and mean-centering
- Eigenvalue decomposition (EVD)
- Singular value decomposition (SVD)
- Image reconstruction with varying components
