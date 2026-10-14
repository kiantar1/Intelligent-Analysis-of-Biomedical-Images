# HW3: Medical Image Segmentation

This assignment covers segmentation with two approaches: a deep learning model (U-Net) for brain MRI tumors, and a classical, pipeline-based approach in CellProfiler for tumors in fluorescence lung tissue images.

## Part 1: U-Net for Brain MRI Tumor Segmentation (`IABI_UNET.ipynb`)

- **Dataset:** [LGG MRI Segmentation](https://www.kaggle.com/datasets/mateuszbuda/lgg-mri-segmentation) (brain MRI slices with FLAIR abnormality masks), split 80/10/10 into train/validation/test
- **Pipeline:** custom PyTorch `Dataset` with resizing and augmentations (rotation, flipping)
- **Model:** U-Net implemented from scratch with an encoder-decoder structure, batch normalization, and skip connections
- **Loss & metrics:** Dice loss, Dice coefficient and IoU, chosen because tumors occupy a small fraction of each image
- **Training:** 50 epochs with best-checkpoint saving based on validation loss, followed by qualitative visualization of predictions vs. ground truth

### Test Results

| Metric | Value |
|---|---|
| Dice | 0.807 |
| IoU | 0.682 |
| Pixel Accuracy | 0.996 |

The near-perfect pixel accuracy versus a Dice of 0.81 shows why accuracy is misleading here: background pixels dominate, so a model can score high accuracy while missing much of the tumor.

## Part 2: Tumor Detection with CellProfiler (`IABI_HW3_P2_Report.pdf`)

A CellProfiler pipeline that detects and outlines tumors in a mouse lung tissue sample using a brightfield image and a fluorescence image:

1. **NamesAndTypes:** assign the two images by filename rules
2. **ColorToGray:** convert the lung image by combining all channels, and the fluorescence image by keeping only the green channel, where the tumor marker signal is
3. **IdentifyPrimaryObjects:** segment tumors with Minimum Cross-Entropy thresholding and intensity-based declumping
4. **MeasureObjectSizeShape:** measure the size and shape of detected tumors
5. **ImageMath:** blend the two grayscale images
6. **OverlayOutlines & SaveImages:** draw tumor outlines on the blended image and save the result

The report (in Persian) documents each module's settings and the reasoning behind them, along with intermediate and final outputs.

## Files

| File | Description |
|---|---|
| `IABI_UNET.ipynb` | U-Net brain MRI segmentation |
| `IABI_HW3_P2_Report.pdf` | CellProfiler pipeline report |

The LGG dataset must be downloaded from Kaggle; the notebook expects it at `/kaggle/input/lgg-mri-segmentation/kaggle_3m`. Part 2 requires [CellProfiler](https://cellprofiler.org/).
