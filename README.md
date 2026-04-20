# Non-Invasive MGMT Prediction via Peritumoral Radiomics

---
*Developed as a digital initiative to integrate Artificial Intelligence and predictive molecular modeling into clinical neuroradiology.*

[![Python](https://img.shields.io/badge/Python-3.12+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Dataset](https://img.shields.io/badge/Dataset-BraTS_2021-orange.svg)](https://www.med.upenn.edu/cbica/brats2021/)

This repository contains the complete pipeline for the non-invasive prediction of **MGMT** promoter methylation in Glioblastomas (GBM), utilizing an optimized machine learning approach focused on habitat radiomics.

---

## Author

**Rafael Boava Souza, MD** *Diagnostic Radiology Resident*

* **Current Affiliation:** Federal University of São Paulo (**UNIFESP**), Brazil.

---

## Overview
MGMT methylation is a critical biomarker for predicting response to Temozolomide. This project investigates whether the molecular signature of MGMT is manifested in the microstructural heterogeneity of the **peritumoral edema (FLAIR)** compared to the **tumor core (T1Gd)**.

By utilizing a cohort of **577 patients** (BraTS 2021), this study employs a leakage-free pipeline to demonstrate that radiomic features provide predictive value across different tumor compartments, supporting the role of the tumor microenvironment in molecular characterization.

## Methodology & Rigor
The pipeline implements:
* **Feature Selection:** LASSO (L1 Regularization) integrated within the cross-validation loop to identify robust predictors while preventing data leakage.
* **Validation:** 5-Fold Stratified Cross-Validation and Grid Search for SVM, Random Forest, and XGBoost hyperparameter tuning.
* **Statistical Comparison:** **DeLong Test** used to assess the significance of the difference between habitat performances (Core vs. Edema).

## Performance Results
The benchmark below displays the performance of each algorithm across the two habitats on the independent test set.

### **Algorithm Benchmark**
| Model | Habitat | AUC (Independent Test Set) |
| :--- | :--- | :--- |
| **SVM (RBF)** | **Peritumoral Edema** | **0.632** |
| **SVM (RBF)** | Tumor Core | 0.619 |
| Random Forest | Peritumoral Edema | 0.608 |
| Random Forest | Tumor Core | 0.595 |
| XGBoost | Peritumoral Edema | 0.591 |
| XGBoost | Tumor Core | 0.584 |

### **Key Scientific Findings**
1. **Habitat Consistency:** The **DeLong Test ($p = 0.8648$)** indicates no statistically significant difference between the performance of the Tumor Core and Peritumoral Edema. This suggests that MGMT molecular signatures are pervasive throughout the tumor microenvironment.
2. **Methodological Integrity:** The transition to an integrated feature selection pipeline ensures that metrics reflect realistic generalization, free from the optimistic bias of data leakage.

---

## Visual Results

### Dataset Distribution
Class balance for MGMT methylation status in the study cohort.
![Dataset Distribution](results/dataset_distribution.png)

### Comparative ROC Curves
Performance comparison between habitats with DeLong statistical validation.
![Comparative ROC Curve](results/comparative_roc_curve.png)

### Model Stability
Stability of the SVM model across the 5-fold cross-validation process.
![Model Stability Boxplot](results/model_stability_boxplot.png)

### LASSO Feature Importance
Top 10 radiomic predictors identified by LASSO for both Tumor Core and Peritumoral Edema habitats.
![LASSO Feature Importance](results/lasso_feature_importance.png)

### AUC Comparison
Benchmark of AUC scores across different machine learning algorithms.
![AUC Comparison Bar](results/auc_comparison_bar.png)

### Confusion Matrix
Detailed performance metrics of the best-performing SVM model.
![Confusion Matrix](results/confusion_matrix.png)

---

## Repository Structure
* `MGMT_Prediction_Optimized_Pipeline.ipynb`: Main notebook with integrated LASSO selection and benchmarking.
* `/results`: Contains all performance visualizations and statistical plots.

## How to Run
1. Clone this repository.
2. Install the dependencies:
   ```bash
   pip install -r requirements.txt
