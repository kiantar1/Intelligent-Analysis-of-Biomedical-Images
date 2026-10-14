# HW2: CT Reconstruction & Medical Image Classification

This assignment has two parts: reconstructing CT images from sinograms with a learned denoiser, and classifying medical images across multiple modalities with CNNs.

## Part 1: From Sinograms to CT Images (`FromSinogram_To_Image.ipynb`)

- **Synthetic dataset:** 1,000 randomized 128×128 phantoms built from Shepp–Logan and random ellipses
- **Radon transform from scratch:** forward projection by rotating the image and summing along columns, plus a discussion of the Fourier Slice Theorem
- **Realistic acquisition:** low-dose Poisson noise and limited-angle sinograms
- **Filtered Backprojection (FBP):** frequency-domain filtering of projections followed by backprojection, comparing different filters
- **Learned denoising:** (noisy FBP → ground truth) pairs with 60 views, used to train a lightweight U-Net denoiser with L1 and L2 losses, evaluated with side-by-side comparisons and error maps

## Part 2: Multi-Modality Classification with MedMNIST (`MedMNIST.ipynb`)

| Modality | Dataset | Task |
|---|---|---|
| X-ray | PneumoniaMNIST | Binary classification |
| Ultrasound | BreastMNIST | Binary classification |

- Dataset loading, sample grids, and class-imbalance analysis across splits
- Modality-aware preprocessing and augmentations (e.g. mild CLAHE for X-ray, subtle augmentations for ultrasound), visualized before and after
- Comparison of a **SmallCNN** and a **SmallResNet** (with skip connections) on each dataset
- Evaluation with accuracy, ROC-AUC, confusion matrices, and ROC curves

### Test Results

| Dataset | Model | Accuracy | AUC |
|---|---|---|---|
| PneumoniaMNIST | SmallCNN | 0.869 | 0.940 |
| PneumoniaMNIST | SmallResNet | **0.897** | **0.956** |
| BreastMNIST | SmallCNN | 0.622 | 0.805 |
| BreastMNIST | SmallResNet | **0.853** | **0.861** |

SmallResNet outperforms SmallCNN on both datasets, with the largest gap on the small, imbalanced BreastMNIST.

## Files

| File | Description |
|---|---|
| `FromSinogram_To_Image.ipynb` | CT reconstruction (Radon, FBP) and U-Net denoiser |
| `MedMNIST.ipynb` | Multi-modality CNN classification |
