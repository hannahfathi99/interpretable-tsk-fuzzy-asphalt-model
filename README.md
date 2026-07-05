# TSK Fuzzy Inference System for Asphalt Performance Prediction

Python | Jupyter Notebook | Fuzzy Logic | Takagi–Sugeno–Kang (TSK) Model | Fuzzy C-Means | Explainable AI | Engineering Regression

---

## Overview

This repository presents a complete implementation of a **Takagi–Sugeno–Kang (TSK) fuzzy inference system** for predicting key performance characteristics of asphalt mixtures.

The system is designed as an end-to-end **interpretable machine learning pipeline** for civil engineering applications, combining fuzzy logic, clustering-based rule generation, and regression learning.

Unlike conventional black-box models, this framework prioritizes **transparency, interpretability, and rule-based reasoning**.

---

## Problem Statement

The goal is to predict the following asphalt performance indicators:

- **Stability (kN)** – load-bearing capacity  
- **Flow (mm)** – deformation behavior under stress  
- **ITSM @ 20°C (MPa)** – stiffness at moderate temperature  
- **ITSM @ 30°C (MPa)** – stiffness at high temperature  

using 10 mix design and volumetric properties.

---

## Research Motivation

Most machine learning models used for asphalt performance prediction rely on black-box approaches such as Artificial Neural Networks (ANN), Support Vector Regression (SVR), and Random Forests. While these methods often achieve high predictive accuracy, they provide limited interpretability and fail to explicitly capture the underlying physical relationships in pavement engineering.

In contrast, this work develops an **interpretable fuzzy regression framework** based on Takagi–Sugeno–Kang (TSK) fuzzy systems.

This enables:

- Transparent rule extraction from data-driven clusters  
- Human-readable IF–THEN decision structures  
- Local linear interpretability within fuzzy regions  
- Strong alignment with engineering domain knowledge  

---

## Engineering Relevance

Accurate prediction of asphalt mixture performance is essential in pavement engineering and infrastructure design.

This work contributes to:

- Improving road safety and structural durability  
- Optimizing asphalt mix composition during design  
- Reducing experimental laboratory cost and time  
- Supporting data-driven civil engineering decision systems  
- Enhancing sustainability in road construction through predictive modeling  

---

## Methodological Contribution

This implementation introduces a fully modular TSK fuzzy inference pipeline with the following contributions:

- Output-specific feature selection for multi-target interpretability  
- Fuzzy C-Means (FCM) based adaptive rule generation  
- Cross-validation-based optimization of rule complexity  
- Hybrid fuzzy-regression learning with first-order consequents  
- Fully transparent inference structure without black-box optimization  

Unlike standard ANFIS implementations, this system explicitly controls:

- Rule structure  
- Feature subsets per output  
- Model complexity via rule tuning  

This makes the framework suitable for both prediction and engineering knowledge extraction.

---

## Baseline Comparison (Recommended Extension)

This framework can be compared against standard machine learning regression models such as:

- Artificial Neural Networks (ANN)  
- Support Vector Regression (SVR)  
- Random Forest Regression (RF)  

This comparison highlights the trade-off between:

- **Accuracy (black-box models)**  
- **Interpretability (TSK fuzzy system)**  

---

## Input Features

### Binder Properties
- Viscosity (η)  
- Asphalt Content (%Pb)  
- Effective Asphalt Content (Pbe)  

### Volumetric Properties
- Maximum Theoretical Specific Gravity (Gmm)  
- Unit Weight  
- Air Voids (Va)  

### Aggregate Gradation
- P200 (fines content)  
- P4 (coarse skeleton indicator)  
- P38 (intermediate aggregate fraction)  
- P34 (large aggregate fraction)  

---

## Methodology Pipeline

The system follows a structured fuzzy modeling pipeline:

```

Raw Data
      ↓
Data Cleaning & Physical Constraints
      ↓
Train/Test Split (80/20)
      ↓
Standardization (Z-score scaling)
      ↓
Feature Selection (ANOVA F-test per target)
      ↓
Fuzzy C-Means Clustering (rule generation)
      ↓
Gaussian Membership Function Construction
      ↓
TSK Rule Formation
      ↓
Weighted Least Squares (consequent learning)
      ↓
Cross-Validation (rule tuning)
      ↓
Model Evaluation (RMSE)

```

---

## TSK Fuzzy Model Structure

### 1. Rule Antecedent (Fuzzy Partitioning)

Each rule is derived using **Fuzzy C-Means clustering**, where each cluster defines a fuzzy region of the input space.

### 2. Gaussian Membership Function

The degree of membership is defined as:

$$
\mu_j(x) = \exp\left(-\frac{\|x - c_j\|^2}{2\sigma_j^2}\right)
$$

where:

- $c_j$ : cluster center  
- $\sigma_j$ : spread parameter 

---

### 3. Consequent Model (First-Order Linear Function)

Each fuzzy rule outputs a local linear model:

$$
f_j(x) = a_{j0} + \sum_{i=1}^{n} a_{ji} x_i
$$

---

### 4. Final Prediction

The final output is computed as a weighted aggregation:

$$
\hat{y}(x) = \sum_{j=1}^{R} w_j(x)\, f_j(x)
$$

where:

- $w_j(x)$ : normalized firing strength 

---

## Feature Selection Strategy

For each output variable, the top-5 features are selected using:

- **ANOVA F-test (f_regression)**  
- Output-specific ranking  

This ensures:
- Reduced dimensionality  
- Better generalization  
- Improved interpretability  

---

## Model Training Strategy

Each target variable is modeled independently:

- Stability → independent TSK system  
- Flow → independent TSK system  
- ITSM20 → independent TSK system  
- ITSM30 → independent TSK system  

Each system has:
- Custom feature subset  
- Optimized rule count  
- Independent training process  

---

## Rule Optimization

The number of fuzzy rules is selected using **K-Fold Cross Validation**.

Candidate values:
```

[3, 5, 7, 9, 11]

```

Selection criterion:
- Minimum average RMSE across folds

---

## Evaluation Metrics

Performance is evaluated using:

- Root Mean Squared Error (RMSE)
- Train vs Test comparison
- Scatter plot analysis (Predicted vs Actual)

---

## Key Results (Summary)

- Strong alignment between predicted and actual values  
- Low generalization gap (train vs test RMSE)  
- Gaussian membership functions provide stable performance  
- Feature selection significantly improves robustness  
- Higher ITSM targets require more rules due to increased nonlinearity  

---

## Repository Structure

```

Fuzzy-TSK-Asphalt-System/

├── data/
│   └── Asphalt-Dataset-ToClass.xlsx
│
├── notebooks/
│   └── Fuzzy_project_2.ipynb
│
├── reports/
│   ├── Project2-report.pdf
│   └── Prj2-dataset description.pdf
│
├── outputs/
│   └── figures/
│
├── README.md
├── requirements.txt
├── LICENSE
└── .gitignore

````

---

## How to Run

### 1. Install dependencies

```bash
pip install -r requirements.txt
````

### 2. Run notebook

Open:

```
Fuzzy_project_2.ipynb
```

All steps including preprocessing, training, evaluation, and visualization are fully automated.

---

## Requirements

```
numpy
pandas
scikit-learn
matplotlib
seaborn
scikit-fuzzy
pickle-mixin
```

---

## Key Features of This Project

* Fully from-scratch TSK fuzzy implementation
* Fuzzy C-Means based rule generation
* Per-output adaptive feature selection
* Cross-validation based rule tuning
* Interpretable rule-based regression system
* Engineering-driven modeling pipeline

---

## Interpretability

Unlike black-box models, this system provides:

* Explicit fuzzy IF–THEN rules
* Local linear interpretability
* Cluster-based reasoning
* Transparent decision structure

This makes it suitable for **engineering decision support systems**.

---

## Limitations

* Sensitive to clustering initialization
* Computational cost increases with rule number
* Linear consequents may underfit highly nonlinear regions

---

## Future Work

* ANFIS-based hybrid optimization
* Evolutionary rule optimization (GA / PSO)
* Uncertainty-aware fuzzy modeling
* Deployment as interactive engineering tool

---

## Citation

If you use this work, please cite:

```
Hannah Fathi (Fall 2025). TSK Fuzzy Inference System for Asphalt Performance Prediction.
```

---

## Author

**Hannah Fathi**

M.Sc. Artificial Intelligence

Shiraz University

Research Interests:

* Explainable AI
* Computer Vision
* Remote Sensing
* Medical AI
* Large Language Models

---

## License

This project is released under the **MIT License**.
