# Intelligent Analysis of Biomedical Images

Course assignments and poster session materials for **Intelligent Analysis of Biomedical Images** at Sharif University of Technology.

## Repository Structure

| Folder | Topic | Contents |
|---|---|---|
| [`HW1`](./HW1) | Classical image processing | SVD-based image compression and FFT-based frequency-domain filtering |
| [`HW2`](./HW2) | CT reconstruction & medical image classification | Radon transform and filtered back-projection from scratch on synthetic Shepp–Logan phantoms, a small DL denoiser, and CNN classification across multiple modalities with MedMNIST |
| [`HW3`](./HW3) | Segmentation | U-Net for brain MRI tumor segmentation (Dice/IoU), and a CellProfiler pipeline for tumor detection in fluorescence lung tissue images |
| [`HW4`](./HW4) | Registration & graph learning | VoxelMorph for unsupervised deformable image registration, and Graph Neural Networks for biomedical data |
| [`Poster-Session`](./Poster-Session) | Paper presentation | Poster reviewing *ScribFormer: A Transformer-CNN Hybrid Network for Scribble-Supervised Medical Image Segmentation* (Meng et al., IEEE TMI 2023): a hybrid CNN-Transformer model with Feature Coupling Units and attention-guided CAMs for weakly-supervised cardiac MRI segmentation |

## Tools & Libraries

Python, NumPy, SciPy, scikit-image, Matplotlib, PyTorch, MedMNIST, CellProfiler

## Running the Notebooks

Each notebook is self-contained. Install the dependencies listed at the top of each notebook.

Some assignments require external datasets that are not included in this repository; download instructions are inside the corresponding notebooks.

## Credits

- The poster summarizes the work of X. Meng, Z. Wang, Y. Li, et al. ([ScribFormer, IEEE TMI 2023](https://doi.org/10.1109/TMI.2024.3363190)); all methods and results belong to the original authors.
