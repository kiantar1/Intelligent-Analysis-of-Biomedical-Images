# HW4: Graph Neural Networks & Deformable Image Registration

This assignment has two parts: implementing Graph Convolutional Networks from scratch, and training VoxelMorph for unsupervised deformable registration of medical images.

## Part 1: Graph Neural Networks (`GNN_Practical.ipynb`)

- **Dataset:** Cora citation graph (via PyTorch Geometric), node classification
- **Custom GCN layer:** a `GCNConv` built on `MessagePassing` that supports k-hop neighborhood aggregation
- **Architectures compared:**
  - **Stacked GCN:** K layers, each aggregating 1-hop neighbors
  - **Single k-hop GCN:** one layer that aggregates k-hop neighbors directly
- **Experiment:** test accuracy of both architectures for K = 1 to 5, showing how depth vs. receptive-field size affects performance
- **Visualization:** t-SNE of hidden node embeddings across training epochs
- **Result:** the 2-layer Stacked GCN reaches **80.1%** test accuracy

### Theory Conclusions
*(The theory part of this assignment was submitted as a handwritten report.)*

- **Graph isomorphism:** two given graphs were shown to be isomorphic by constructing an explicit node mapping that preserves all edges.
- **Aggregation functions:** a counterexample shows that **max** and **mean** aggregators can fail to distinguish different neighborhoods, while **sum** succeeds, so sum is the most expressive of the three.
- **Expressiveness:** an inductive proof shows that if the Weisfeiler-Lehman (WL) test cannot distinguish two graphs, a message-passing GNN cannot either; GNNs are at most as powerful as the WL test.

## Part 2: Image Registration with VoxelMorph (`voxelmorph_notebook.ipynb`)

- **Dataset:** HeadCT images from MedNIST (via MONAI), with fixed/moving pairs created through random affine transforms
- **Model:** VoxelMorph (`VxmDense`), a U-Net that predicts a dense deformation field, applied with a Spatial Transformer
- **Implemented components:**
  - Similarity loss (MSE / local cross-correlation)
  - Gradient-based smoothness regularization of the flow field
  - Combined loss: `L_total = L_sim + λ · L_smooth`
  - Training and validation loops, and visualization of fixed / moving / registered images with the flow field
- **Experiments:** two-stage training with λ = 0.001 (15, then 40 epochs), compared against λ = 0.1

### Validation Results (40 epochs)

| λ (smoothness) | Val Dice |
|---|---|
| 0.001 | 0.886 |
| 0.1 | 0.889 |

### Analysis Conclusions
*(The analysis for this part was submitted as a handwritten report.)*

- **Scope of registration:** VoxelMorph can correct geometric differences such as translation, rotation and local deformation, but not intensity differences between images.
- **Short training (Stage 1):** after 15 epochs the model barely changed the moving images and failed on rotated samples, with a noisy, abrupt flow field, attributed to underfitting, the choice of λ, and possible local minima.
- **Effect of λ:** increasing λ from 0.001 to 0.1 produced a much smoother and more continuous flow field with fewer abrupt changes, lowering the risk of folding. Small λ gives the model more freedom and tends to overfit pixel displacements, while large λ constrains it and can underfit.
- **Dice:** final Dice is nearly the same for both settings, but λ = 0.1 reaches it with a more physically plausible deformation.
- **Extension:** adding a Dice loss on warped segmentation masks (`L_total = L_sim + λ·L_smooth + γ·L_dice`) would make training weakly supervised and guide the model toward anatomically correct alignment, especially in low-contrast or noisy regions.

## Files

| File | Description |
|---|---|
| `GNN_Practical.ipynb` | Stacked vs. k-hop GCNs on Cora |
| `voxelmorph_notebook.ipynb` | VoxelMorph deformable registration on HeadCT |
