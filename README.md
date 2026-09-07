# BRCA Gene Expression: Clustering & Classification

Unsupervised and supervised analysis of RNA-seq gene expression data (RPKM) from breast tumor and normal tissue samples, comparing how well expression structure alone recovers known Tumor/Normal labels, and benchmarking multiple classifiers for predicting tissue type from expression profiles.

## Overview

This project runs a full pipeline on a gene-expression matrix (~20,500 genes × ~880 samples):

1. **Preprocessing** — load and reshape raw RPKM matrix, filter low-expression/zero-variance genes, handle missing values
2. **Descriptive statistics** — per-gene mean/median/SD, per-sample library totals
3. **Transformation & dimensionality reduction** — log2 transform, PCA
4. **Unsupervised clustering** — k-means and hierarchical clustering on PCA-reduced scores; silhouette score for cluster quality
5. **Consensus clustering** — feature selection, k-means- and hierarchical-based consensus clustering, Proportion of Ambiguous Clustering (PAC) for choosing *k*, agreement with true labels via Adjusted Rand Index (ARI)
6. **Classification** — train/test split, four classifiers trained and compared:
   - Random Forest
   - Support Vector Machine (SVM)
   - k-Nearest Neighbors (kNN)
   - Elastic Net logistic regression (glmnet)
7. **Model evaluation** — confusion matrices, accuracy/sensitivity/specificity comparison, ROC curves and AUC, 5-fold cross-validation on the Random Forest (tuning `mtry`)

## Repository structure

```
analysis/
  brca_gene_expression_analysis.Rmd   # full pipeline, steps 1–30
data/                                  # not included — see Data below
```

## Data

The analysis expects an RPKM gene-expression matrix (`data/brca.csv`) with samples as columns and genes as rows, following the standard TCGA BRCA RNA-seq RPKM layout (row 1: sample IDs, row 2: measurement type, remaining rows: genes). The raw data file is not included in this repository; place your own copy at `data/brca.csv` before knitting.

## Methods & tools

R, with `readr`, `cluster`, `caret`, `randomForest`, `e1071`, `class`, `pROC`, `glmnet`.

## Author

Promise Bansah — MPhil Biodata Analytics and Computational Genomics, KNUST
