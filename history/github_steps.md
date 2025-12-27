# Git History Reconstruction: Image PCA Eigencats

This document describes the realistic development history for the Image PCA & Eigencats Analysis project. Each step represents a believable checkpoint in the project's evolution from initial repository setup to a portfolio-ready state.

---

## History Expansion Note

**Previous run:** 6 steps (step_01 through step_06)
**Current run:** 10 steps (step_01 through step_10)
**Multiplier achieved:** 10 / 6 = 1.67× (exceeds minimum 1.5× requirement)

### Mapping from Old Steps to New Steps

The expansion was achieved through two strategies:

**Strategy A - Splitting large commits:**
- **Old step 02** (Core PCA/EVD) → **New steps 02-03** (split into utility functions + EVD implementation)
- **Old step 03** (SVD + reconstruction) → **New steps 04, 07** (separated SVD from reconstruction)

**Strategy B - Oops→hotfix sequence:**
- **New step 05** (OOPS): Introduced bug in SVD formula (wrong axis for mean calculation)
- **New step 06** (HOTFIX): Fixed the SVD calculation bug

**Preserved steps (conceptually similar):**
- Old step 01 → New step 01 (initial setup)
- Old step 04 → New step 08 (dataset integration)
- Old step 05 → New step 09 (comprehensive documentation)
- Old step 06 → New step 10 (portfolio refinement)

### Oops→Hotfix Details

**What broke (Step 05):**
In the SVD implementation, I incorrectly computed the mean along axis=1 instead of axis=0, which caused the mean-centering to produce wrong results. The eigencats looked distorted and the reconstruction quality was poor.

**How I noticed:**
When visualizing the reconstructed images, they appeared heavily distorted with strange artifacts. Compared the output to the EVD approach and noticed significant discrepancies. Traced back through the code and found the axis parameter error in the mean calculation.

**What fixed it (Step 06):**
Changed `cats.mean(axis=1)` to `cats.mean(axis=0)` in the SVD preprocessing section. This correctly computes the mean across all images (axis 0) rather than within each image (axis 1). After the fix, SVD and EVD produced identical results as expected.

---

## Development Timeline Overview

The project evolved through 10 main stages:
1. **Initial Repository Setup** - Basic project scaffolding
2. **Utility Functions** - Helper functions for data processing
3. **Core EVD Implementation** - Eigenvalue decomposition for PCA
4. **SVD Implementation** - Alternative approach using singular value decomposition
5. **Bug in SVD** - Incorrect axis parameter (realistic mistake)
6. **Hotfix for SVD** - Corrected axis parameter
7. **Image Reconstruction** - Demonstrate dimensionality reduction
8. **Dataset Integration** - Add cat face data
9. **Comprehensive Documentation** - README and inline docs
10. **Portfolio Refinement** - Professional cleanup and standardization

---

## Step 01: Initial Repository Setup

**Commit Message:** `Initial commit: Set up repository structure`

**Description:**
Created the initial repository with basic Python project structure. Set up .gitignore to exclude common Python artifacts, virtual environments, and Jupyter checkpoints. Added a minimal README with project title and placeholder description. Initialized requirements.txt with core scientific Python dependencies.

**Files Added:**
- `README.md` - Initial project description
- `requirements.txt` - Python dependencies (NumPy, Matplotlib, Jupyter)
- `.gitignore` - Python/Jupyter ignore patterns

**Developer Mindset:**
Starting a new computer vision project to explore PCA on image data. Setting up the basic repository structure before diving into implementation.

---

## Step 02: Add Utility Functions

**Commit Message:** `Add utility functions for data preprocessing`

**Description:**
Created the Jupyter notebook and added essential utility functions. Implemented `plot_cats()` for visualizing cat faces in a grid layout and `sort_eigvectors()` for ordering eigenvectors by their eigenvalues. These helper functions will be used throughout the analysis.

**Files Added/Modified:**
- `eigencats.ipynb` - Created with:
  - Introduction and setup cells
  - `plot_cats()` function for grid visualization
  - `sort_eigvectors()` utility for sorting eigenvectors by eigenvalues

**Developer Mindset:**
Building the foundation with utility functions first. Want to establish visualization helpers before implementing the core algorithms so I can easily debug and verify results as I go.

---

## Step 03: Implement Eigenvalue Decomposition

**Commit Message:** `Add PCA implementation with eigenvalue decomposition`

**Description:**
Implemented the core preprocessing and eigenvalue decomposition functions. Created `preprocess()` for mean-centering and reshaping data, and `eigencats_evd()` for computing principal components using NumPy's eigendecomposition. Added code cells to load hypothetical data, compute eigencats, and visualize the first four components.

**Files Modified:**
- `eigencats.ipynb` - Added:
  - `preprocess()` function for mean-centering and flattening
  - `eigencats_evd()` function for eigendecomposition
  - Markdown cells explaining the EVD approach
  - Code cells for EVD computation and visualization

**Developer Mindset:**
Building the mathematical foundation. Implementing PCA from scratch using NumPy's eigendecomposition to understand the underlying linear algebra. Starting with EVD as it's more intuitive - will add SVD later for comparison.

---

## Step 04: Implement Singular Value Decomposition

**Commit Message:** `Add SVD approach for computing eigencats`

**Description:**
Extended the notebook with an alternative SVD-based approach to compute eigencats. Implemented `eigencats_svd()` function that uses NumPy's singular value decomposition. Added markdown documentation explaining how SVD relates to PCA and why both methods should produce equivalent results.

**Files Modified:**
- `eigencats.ipynb` - Added:
  - `eigencats_svd()` function using singular value decomposition
  - Markdown cells explaining SVD approach
  - Code cells demonstrating SVD computation

**Developer Mindset:**
Exploring the SVD approach as an alternative to EVD. Want to show both methods produce equivalent results. SVD is often more numerically stable and efficient for large datasets.

---

## Step 05: Bug in SVD Implementation

**Commit Message:** `Add reconstruction examples with SVD [contains bug]`

**Description:**
Added image reconstruction functionality using the SVD approach. Implemented `reconstruct_cats()` function to demonstrate how faces can be rebuilt from principal components. However, introduced a bug in the SVD preprocessing: used `cats.mean(axis=1)` instead of `cats.mean(axis=0)`, which computes the mean incorrectly. This bug won't be immediately obvious until testing.

**Files Modified:**
- `eigencats.ipynb` - Added:
  - `reconstruct_cats()` function for varying-fidelity reconstruction
  - Code cells demonstrating reconstruction with 10, 40, and 80 components
  - **Bug**: Mean computation uses wrong axis in SVD section

**Developer Mindset:**
Adding reconstruction to show dimensionality reduction in action. Excited to see how few components are needed for recognizable faces. Made a careless mistake with the axis parameter - happens when coding quickly.

---

## Step 06: Fix SVD Axis Bug

**Commit Message:** `Fix: Correct axis parameter in SVD mean calculation`

**Description:**
Fixed the bug introduced in the previous commit. Changed `cats.mean(axis=1)` to `cats.mean(axis=0)` in the SVD preprocessing section. The reconstructions now look correct and match the EVD approach. Verified both methods produce identical eigencats.

**Files Modified:**
- `eigencats.ipynb` - Fixed:
  - Corrected axis parameter in mean calculation: `axis=1` → `axis=0`
  - SVD now correctly computes mean across all images

**Developer Mindset:**
Noticed the reconstructed images looked distorted. Debugged by comparing EVD and SVD outputs. Found the axis error - obvious in hindsight! This is why it's important to implement multiple approaches for verification.

---

## Step 07: Add Image Reconstruction Analysis

**Commit Message:** `Add comprehensive reconstruction analysis and visualization`

**Description:**
Enhanced the reconstruction section with better visualization and analysis. Added code to compare reconstruction quality with varying numbers of components (10, 40, 80). Created comparison grids showing original vs reconstructed images. Added markdown explaining the trade-off between compression and quality.

**Files Modified:**
- `eigencats.ipynb` - Enhanced:
  - More detailed reconstruction visualizations
  - Comparison grids of original vs reconstructed
  - Markdown analysis of reconstruction quality
  - Discussion of compression trade-offs

**Developer Mindset:**
Now that the algorithms work correctly, focusing on demonstrating the dimensionality reduction concept. Want to show how few components are needed for good reconstruction - this is the key insight of PCA.

---

## Step 08: Add Dataset and Reference Visualizations

**Commit Message:** `Add cat face dataset and reference images`

**Description:**
Integrated the cat face dataset (80 images, 64×64 grayscale) as a NumPy binary file for efficient loading. Created reference visualizations showing expected outputs: the mean cat face and sample eigencats. These serve as both documentation and verification that the implementation produces correct results. Updated code cells to load the actual dataset instead of using placeholders.

**Files Added:**
- `cats.npy` - Cat face image dataset (80 images, 64×64 pixels)
- `imgs/meancat.png` - Reference visualization of mean cat face
- `imgs/eigencats.png` - Reference visualization of principal eigencats

**Files Modified:**
- `eigencats.ipynb` - Updated to load actual data from `cats.npy`

**Developer Mindset:**
Now that the algorithms work, adding the actual dataset and generating reference images to document expected outputs. This makes it easier for others (and future me) to verify the implementation is working correctly.

---

## Step 09: Comprehensive Documentation

**Commit Message:** `Add comprehensive documentation and analysis`

**Description:**
Enhanced the notebook with detailed markdown cells explaining each section. Added mathematical formulas, methodological notes, and analytical discussion comparing EVD and SVD approaches. Updated README with complete setup instructions, folder structure, data format documentation, reproducibility notes, and troubleshooting guide. The project is now well-documented and ready to share.

**Files Modified:**
- `eigencats.ipynb` - Added extensive markdown documentation:
  - Introduction explaining eigencats concept with references
  - Mathematical formulas for covariance matrix and eigendecomposition
  - Section headers: Preprocessing, EVD, SVD, Reconstruction, Analysis
  - Explanatory text for each implementation section
  - Analysis discussing EVD/SVD equivalence
- `README.md` - Expanded to include:
  - Complete problem and approach description
  - Tech stack details
  - Folder structure diagram
  - Installation and usage instructions
  - Data format and location information
  - Expected outputs description
  - Reproducibility notes
  - Troubleshooting section

**Developer Mindset:**
Time to make this accessible to others. Adding thorough documentation so anyone can understand the methodology, run the code, and interpret results. Good documentation is key for portfolio projects and potential collaborators.

---

## Step 10: Portfolio Refinement and Professional Cleanup

**Commit Message:** `Refine for portfolio: remove assignment artifacts and standardize`

**Description:**
Final polish pass to transform the project from exploratory/educational code into a portfolio-ready demonstration. Removed all assignment-style language ("Step 1", "Step 2", imperative instructions). Changed markdown cells from instructional tone to descriptive/explanatory narrative. Updated README to reflect repository root structure (removed reference to assignment folder "2.3/"). Ensured all documentation uses professional, descriptive language suitable for a public portfolio.

**Files Modified:**
- `eigencats.ipynb` - Reframed all markdown cells:
  - Removed "Step N:" prefixes from section headers
  - Changed imperative instructions ("Compute...", "Plot...") to descriptive text
  - Converted assignment questions ("What do you notice?") to explanatory prose
  - Restructured analysis section from Q&A format to cohesive explanation
- `README.md` - Updated references:
  - Changed folder structure from "2.3/" to "image-pca-eigencats/"
  - Updated path instructions from "cd 2.3" to proper repo-relative paths

**Files Added:**
- `project_identity.md` - Professional project identity documentation
- `report.md` - Execution log of portfolio transformation
- `suggestion.txt` - Ledger of identified issues
- `suggestions_done.txt` - Ledger of applied changes

**Developer Mindset:**
Preparing this project for public portfolio. Removing any traces of its academic origins and ensuring the documentation reads as a professional demonstration. Want viewers to see clean, well-documented code that showcases understanding of PCA and computer vision fundamentals.

---

## Development Notes

**Total Development Time:** Estimated 3-4 days of focused work
- Day 1: Setup + utility functions + EVD (Steps 1-3)
- Day 2: SVD implementation + bug discovery and fix (Steps 4-6)
- Day 3: Reconstruction + data integration (Steps 7-8)
- Day 4: Documentation + portfolio refinement (Steps 9-10)

**Technologies Used:**
- Python 3.6+ with NumPy for numerical computation
- Matplotlib for visualization
- Jupyter Notebook for interactive development and presentation
- Git for version control

**Key Design Decisions:**
1. Implemented both EVD and SVD approaches to demonstrate mathematical equivalence
2. Used NumPy binary format for efficient dataset storage
3. Included reference images for output verification
4. Structured as notebook for educational/demonstration purposes
5. Kept dependencies minimal (numpy, matplotlib, jupyter only)
6. Built utility functions first for better code organization

**Lessons Learned:**
- Always verify axis parameters in NumPy operations (learned via bug in step 05)
- Having multiple implementations helps catch bugs through cross-validation
- Incremental commits make debugging easier
- Good visualization functions pay off throughout development

---

## Snapshot Structure

Each step is captured as a complete snapshot in `history/steps/step_XX/`:
- `step_01/` - Initial repository setup
- `step_02/` - Utility functions
- `step_03/` - Core EVD implementation
- `step_04/` - SVD implementation
- `step_05/` - Reconstruction with bug
- `step_06/` - Hotfix for SVD bug
- `step_07/` - Enhanced reconstruction analysis
- `step_08/` - Dataset integration
- `step_09/` - Documentation pass
- `step_10/` - Portfolio refinement (matches final state)

**Note:** The `history/` directory itself is not included in snapshots to avoid recursion.
