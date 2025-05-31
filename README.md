# Automated Assessment of Java Code Using CodeT5+, Early Fusion, and CatBoost Regressor

This repository presents a machine learning-based system to automatically assess Java code submitted by students. By integrating CodeT5+ embeddings, early feature fusion techniques, and a CatBoost Regressor, the project provides a scalable and interpretable solution to evaluate code quality on a scale of 0–10.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Authors](#authors)
- [Methodology](#methodology)
  - [Dataset](#dataset)
  - [Feature Engineering](#feature-engineering)
  - [Dimensionality Reduction](#dimensionality-reduction)
  - [Feature Fusion and Scaling](#feature-fusion-and-scaling)
  - [Model Training](#model-training)
- [Results](#results)
- [Installation](#installation)
- [Usage](#usage)
- [License](#license)

## Overview

Manual grading of student-written code is time-consuming and often inconsistent. This project proposes an automated solution using modern NLP techniques tailored for code. The framework predicts a numerical score for submitted Java code, aiding educators with fast, fair, and scalable assessment.

## Features

- Automatic extraction and processing of structural components in Java code
- Use of pre-trained CodeT5+ model for generating code embeddings
- Feature reduction using PCA and Information Gain
- Fusion of code features through concatenation and addition
- Regression models including CatBoost, XGBoost, Random Forest, and others
- Interpretability via SHAP analysis

## Methodology

### Dataset

- 1232 Java code samples solving undergraduate-level problems
- Each sample includes:
  - `Student Submitted Code`
  - `Correct Code` (ground truth)
  - `Final Marks` (integer score from 0 to 10)

### Feature Engineering

- Code split into two primary features:
  - **Keywords**: Syntax tokens, control structures, method signatures
  - **Code Logic**: Custom classes and object-oriented structures
- Features embedded using CodeT5+, a transformer-based code encoder

### Dimensionality Reduction

- **PCA**: Reduces 256-dimensional embeddings to top 20 components
- **Information Gain**: Selects top 20 features relevant to the target score

### Feature Fusion and Scaling

- Features scaled with weights:
  - Keywords: 0.9
  - Code Logic: 0.1
- Fusion techniques:
  - **Addition Fusion**: Element-wise addition of reduced vectors
  - **Concatenation Fusion**: Concatenation of reduced vectors (resulting in 40D)

### Model Training

- Models used: CatBoost, XGBoost, Random Forest, AdaBoost, Decision Tree
- Best performing model: **CatBoost Regressor**
- Evaluation metrics:
  - R² Score
  - RMSE
  - MAPE
- 10-fold cross-validation and hyperparameter tuning applied

## Results

- Best R² on test set: **0.56** (CatBoost, PCA, concatenation fusion)
- Demonstrated 200% improvement over prior work (baseline R²: 0.27)
- SHAP analysis showed Keywords are more influential than Code Logic
- Concatenation fusion offers better interpretability and slightly higher accuracy than addition fusion

| Reduction Technique | Fusion Method    | R² (Test) | RMSE (Test) | MAPE (Test) |
|---------------------|------------------|-----------|-------------|-------------|
| PCA                 | Concatenation    | 0.56      | 1.61        | 33.71       |
| PCA                 | Addition         | 0.52      | 1.70        | 35.32       |
| Information Gain    | Concatenation    | 0.52      | 1.69        | 36.86       |
| Information Gain    | Addition         | 0.51      | 1.71        | 38.23       |

## Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/java-code-assessment.git](https://github.com/pranav11024/Automated-Assessment-of-Java-Code-Using-CodeT5-Early-Fusion-and-CatBoost-Regressor.git
  
