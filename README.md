# CIFAR-10 Unsupervised Image Clustering  
Unsupervised image clustering pipeline using deep feature extraction, dimensionality reduction, and K-Means clustering on the CIFAR-10 dataset. The project includes interactive cluster exploration using a Gradio-based interface.

---

## **Project Overview**

This project applies unsupervised learning to group visually similar images without using labels.  
The pipeline uses:

- **ResNet-18 pretrained on ImageNet** to extract 512-dimensional deep features.
- **PCA** to compress features to 50 dimensions.
- **UMAP** for 2D visualization of image similarity.
- **K-Means (k=10)** to cluster images into meaningful groups.
- **Cosine similarity search** to retrieve visually similar images.
- **Gradio UI** to explore clusters interactively.

This project demonstrates how deep learning embeddings can uncover visual patterns in image data without supervision.

---

## **Key Steps**

### 1. Dataset  
CIFAR-10 (60,000 images, 10 classes, 32×32 resolution).  
Automatically downloaded using `torchvision.datasets.CIFAR10`.

### 2. Feature Extraction  
A pretrained **ResNet-18** is used as a fixed feature extractor.  
The final fully connected layer is removed to produce 512-dim embeddings for each image.

### 3. Dimensionality Reduction  
Two-stage reduction:
- **PCA → 50D**
- **UMAP → 2D** (for visualization)

### 4. Clustering  
K-Means clustering applied on PCA features:
- k = 10  
- n_init = 10  
- Evaluated using Silhouette Score, ARI, and NMI  
- Cluster vs true class distribution analyzed using a contingency matrix

### 5. Visualization  
- UMAP projection of raw features  
- UMAP colored by K-Means clusters  
- UMAP colored by true labels  
- Cluster sample grids  
- Nearest neighbor retrieval using cosine similarity

### 6. Interactive Gradio App  
A simple UI lets users:
- Select a cluster ID  
- View representative image samples from that cluster  
- Explore visual similarity patterns across CIFAR-10

---

## **Results**

### Clustering Insights
- Certain clusters correspond strongly to specific CIFAR-10 classes (e.g., airplanes, ships, trucks).
- Animal classes show more overlap, as expected due to visual similarity.
- Embeddings successfully group similar shapes, textures, and colors.

### Evaluation Metrics (Example)
- Silhouette Score: *~0.04–0.08*  
- ARI and NMI indicate partial alignment with true classes, typical for CIFAR-10.
