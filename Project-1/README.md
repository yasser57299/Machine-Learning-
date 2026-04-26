# 🏥 Early Detection of Sepsis in ICU Patients
### CS4082 Machine Learning · Effat University · Spring 2026

> **Topic 3: Early Detection of Rare Medical Conditions — Minority Class Suppression**

[![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=flat&logo=python&logoColor=white)](https://python.org)
[![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.3+-F7931E?style=flat&logo=scikit-learn&logoColor=white)](https://scikit-learn.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat&logo=jupyter&logoColor=white)](https://jupyter.org)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat)](LICENSE)

---

## 📋 Table of Contents
- [Project Overview](#-project-overview)
- [Adversarial Challenge](#-adversarial-challenge)
- [Dataset](#-dataset)
- [Results](#-results)
- [Project Structure](#-project-structure)
- [Installation](#-installation)
- [Usage](#-usage)
- [Dependencies](#-dependencies)
- [Team](#-team)
- [Links](#-links)

---

## 🔬 Project Overview

Sepsis is a life-threatening condition responsible for **~11 million deaths annually** worldwide. Early detection in ICU patients dramatically improves survival rates, yet it remains extremely challenging due to overlapping symptoms and severe class imbalance in clinical data.

This project builds a **complete machine learning pipeline** for early sepsis detection using real-world ICU time-series data from **40,336 patients**, applying state-of-the-art techniques to handle adversarial class imbalance.

**Key Highlights:**
- 7 classification algorithms compared head-to-head
- SMOTE oversampling + class-weighted training to address minority class suppression
- Patient-level feature engineering from hourly time-series vitals
- Best model: **Random Forest** with AUC-ROC = **0.864** and F1 Macro = **0.730**

---

## ⚠️ Adversarial Challenge

This project directly addresses **Minority Class Suppression** — one of the hardest problems in clinical ML:

| Condition | Count | Percentage |
|-----------|-------|------------|
| No Sepsis | 37,404 | 92.73% |
| Sepsis | 2,932 | **7.27%** |

A naive model predicting "no sepsis" always achieves **92.7% accuracy** while detecting **zero sepsis cases**. Our solution:

1. **SMOTE** — Synthetic Minority Over-sampling Technique (k=5) applied only to training data
2. **class_weight='balanced'** — Penalises minority-class errors more heavily during training
3. **Recall-oriented metrics** — Evaluate using AUC-ROC and F1-sepsis, not raw accuracy

---

## 📊 Dataset

| Property | Value |
|----------|-------|
| Total observations | 1,552,210 hourly rows |
| Unique patients | 40,336 |
| Features (raw) | 15 |
| Features (engineered) | 34 |
| Sepsis rate | 7.27% |
| Train / Test split | 80% / 20% (stratified) |

**Feature Engineering:** For each vital sign (HR, O₂Sat, Temp, SBP, MAP, DBP, Resp), we compute `mean`, `std`, `min`, `max` per patient — capturing both baseline and physiological instability.

---

## 📈 Results

### Test Set Performance (8,068 real patients — imbalanced)

| Model | Precision | Recall | F1 Macro | F1 Sepsis | AUC-ROC |
|-------|-----------|--------|----------|-----------|---------|
| **Random Forest ★** | **0.696** | **0.786** | **0.730** | **0.509** | **0.864** |
| SVM | 0.636 | 0.736 | 0.666 | 0.401 | 0.832 |
| Gradient Boosting | 0.534 | 0.530 | 0.135 | 0.143 | 0.807 |
| Naive Bayes | 0.576 | 0.708 | 0.579 | 0.290 | 0.760 |
| KNN | 0.580 | 0.701 | 0.589 | 0.297 | 0.751 |
| Logistic Regression | 0.563 | 0.693 | 0.547 | 0.259 | 0.749 |
| Decision Tree | 0.537 | 0.631 | 0.472 | 0.197 | 0.631 |

### Best Model — Random Forest Class Breakdown

| Class | Precision | Recall | F1 | Support |
|-------|-----------|--------|----|---------|
| No Sepsis | 0.97 | 0.93 | 0.95 | 7,482 |
| **Sepsis** | **0.42** | **0.64** | **0.51** | **586** |
| Overall Accuracy | — | — | **0.91** | 8,068 |

---

## 📁 Project Structure

```
projectt/
│
├── CS4082_HeartFailure_Prediction.ipynb   # Main notebook (full pipeline)
├── README.md                              # This file
├── requirements.txt                       # Python dependencies
│
├── index.html                             # Portfolio website
├── CS4082_Technical_Report.pdf            # ACL-format technical report
└── CS4082_Poster.pptx                     # Research poster (A1 format)
```

---

## ⚙️ Installation

### 1. Clone the repository
```bash
git clone https://github.com/yasser57299/Machine-Learning-.git
cd Machine-Learning-/projectt
```

### 2. Create a virtual environment (recommended)
```bash
python -m venv venv
source venv/bin/activate        # Mac/Linux
venv\Scripts\activate           # Windows
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

---

## 🚀 Usage

### Run the full pipeline
```bash
jupyter notebook CS4082_HeartFailure_Prediction.ipynb
```

The notebook is divided into clearly labelled sections:
1. **Data Loading & Exploration** — Load and inspect the raw ICU dataset
2. **Feature Engineering** — Aggregate time-series to patient level
3. **Preprocessing** — Imputation, scaling, train/test split
4. **SMOTE** — Rebalance the training set
5. **Model Training & CV** — Train all 7 models with cross-validation
6. **Hyperparameter Tuning** — GridSearchCV on top 3 models
7. **Evaluation** — Full test-set metrics and visualizations

---

## 📦 Dependencies

```
pandas>=1.5.0
numpy>=1.23.0
scikit-learn>=1.3.0
imbalanced-learn>=0.11.0
matplotlib>=3.6.0
seaborn>=0.12.0
jupyter>=1.0.0
```

Install all at once:
```bash
pip install -r requirements.txt
```

---

## 👥 Team

| Name | Student ID | Role |
|------|-----------|------|
| **Yasser Alassad** | S22107723 | Data preprocessing, SMOTE, model training & tuning, GitHub |
| **Umar Ayyash** | S22107722 | Feature engineering, EDA, evaluation, report & portfolio |

**Instructor:** Dr. Naila Marir · `namarir@effatuniversity.edu.sa`  
**Course:** CS4082 Machine Learning · Effat University · Spring 2026

---

## 🔗 Links

| Resource | Link |
|----------|------|
| 🌐 Portfolio Website | [yasser57299.github.io/Machine-Learning-](https://yasser57299.github.io/Machine-Learning-) |
| 📄 Technical Report | [CS4082_Technical_Report.pdf](CS4082_Technical_Report.pdf) |
| 🖼️ Research Poster | [CS4082_Poster.pptx](CS4082_Poster.pptx) |
| 🐙 GitHub Profile | [github.com/yasser57299](https://github.com/yasser57299) |

---

*"The goal is to turn data into information, and information into insight." — Carly Fiorina*
