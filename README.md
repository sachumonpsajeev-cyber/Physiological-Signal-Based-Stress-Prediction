# 🧠 Physiological Signal-Based Stress Prediction

> An end-to-end machine learning pipeline for classifying psychological stress 
> states from raw physiological signals — covering feature extraction, model 
> training, and comparative evaluation.

---

## 📌 Overview

Psychological stress is a major contributor to long-term health deterioration. 
This project builds a supervised ML classification system that detects stress 
states using physiological sensor data, with a full pipeline from raw signal 
processing through to model evaluation.

---

## 🎯 Objectives

- Process and clean raw physiological signal data
- Extract meaningful statistical and frequency-domain features
- Train and compare multiple classification algorithms
- Evaluate model performance using standard metrics (accuracy, F1, ROC-AUC)

---

## 📊 Dataset

| Property | Detail |
|---|---|
| **Type** | Physiological signals (e.g. EDA, HR, temperature) |
| **Task** | Binary / multi-class stress classification |
| **Format** | Time-series sensor recordings |

---

## 🏗️ Pipeline
```
Raw Signal Data
      ↓
Preprocessing & Cleaning
      ↓
Feature Extraction
      ↓
Model Training & Evaluation
      ↓
Results & Comparison
```

---

## 🤖 Models Evaluated

| Model | Notes |
|---|---|
| Logistic Regression | Baseline |
| Random Forest | Ensemble method |
| Support Vector Machine | Kernel-based |
| K-Nearest Neighbours | Distance-based |
| Gradient Boosting | Boosted ensemble |

---

## 📈 Evaluation Metrics
- Accuracy
- Precision / Recall / F1-Score
- ROC-AUC
- Confusion Matrix

---

## 🛠️ Tech Stack
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-F7931E?style=flat&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=flat&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat&logo=jupyter&logoColor=white)

---

## 📁 Repository Structure
```
├── data/               # Raw and processed signal data
├── notebooks/          # Jupyter notebooks for EDA and modelling
├── src/                # Feature extraction and model scripts
├── results/            # Evaluation outputs and plots
└── README.md
```

---

## 👤 Author
**Sachu Mon Puthenpuraickkal Sajeev**  
MSc Data Science & AI — TSI University, Riga, Latvia  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/sachu-mon)
[![WhatsApp](https://img.shields.io/badge/WhatsApp-25D366?style=flat&logo=whatsapp&logoColor=white)](https://wa.me/37122447242)
