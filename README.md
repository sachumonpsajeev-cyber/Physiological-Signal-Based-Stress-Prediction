# 🧠 Physiological Signal-Based Stress Prediction

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-F7931E?style=flat&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![F1 Score](https://img.shields.io/badge/F1%20Score-0.96-brightgreen)
![Real-time](https://img.shields.io/badge/Real--time-Prediction-blue)
![Wearable Data](https://img.shields.io/badge/Data-Wearable%20Sensors-orange)

> End-to-end machine learning pipeline classifying **real-time stress levels** from wearable physiological sensor data — 168,000 rows, 60 engineered features, 0.96 F1-score.

---

## 🎯 Project Goal

Build a system that can:
1. Handle raw wearable physiological data (EDA, BVP, temperature, motion)
2. Engineer meaningful time- and frequency-domain features via windowing
3. Train and compare ML models for multi-class stress classification
4. Deploy a **real-time prediction function** for incoming sensor data

---

## 📊 Results

| Model               | Accuracy | Precision | Recall | F1 Score |
|---------------------|----------|-----------|--------|----------|
| Random Forest ✅    | 0.963    | 0.964     | 0.963  | 0.9635   |
| Decision Tree       | 0.933    | 0.933     | 0.933  | 0.9326   |
| Logistic Regression | 0.660    | 0.625     | 0.660  | 0.5712   |

Best Model: Random Forest — F1-score 0.96 across 3 stress classes (0 = no stress, 1 = moderate, 2 = high)

---

## 🏗️ Pipeline Architecture

Phase 1: Data Loading and Inspection
Shape, missing values, duplicates (28,808 removed), correlation matrix

Phase 2: Preprocessing
Duplicate removal → Column cleaning → Missing value imputation → StandardScaler normalisation → Scaler saved as scaler.joblib

Phase 3: Feature Engineering (Windowing)
Window size: 5 · Step size: 2 · Overlapping windows
→ 60 features per window (10 per signal × 6 signals)
→ Output shape: 69,594 windows × 61 columns

Phase 4: Model Training
80/20 train-test split → Random Forest · Decision Tree · Logistic Regression

Phase 5: Evaluation
Confusion matrices · Feature importance · Model saved as .joblib

Phase 6-7: Real-Time Prediction System
Load model + scaler → Preprocess new data → Window + extract features → Majority vote → Stress level output

---

## 🔬 Feature Engineering

For each of 6 signal columns, 10 features extracted per window:

| Domain      | Features                                              |
|-------------|-------------------------------------------------------|
| Time-Domain | Mean, Std, Min, Max, Median, RMS, Skewness, Kurtosis |
| Frequency   | Dominant Frequency, Spectral Entropy                  |

Total: 60 features per window + target → 61 columns, 69,594 windows

---

## 📁 Dataset

| Property    | Details                                  |
|-------------|------------------------------------------|
| Source      | Physiologicalsignals60sn.csv             |
| Raw rows    | 168,000                                  |
| Signals     | EDA, BVP, Temp, X, Y, Z (motion axes)   |
| Target      | stress_indication (0, 1, 2)              |
| After clean | 139,191 rows (28,809 duplicates removed) |

---

## 🛠️ Tech Stack

- ML: Scikit-learn (RandomForest, DecisionTree, LogisticRegression)
- Data: Pandas, NumPy
- Signal Processing: Custom windowing + FFT-based frequency features
- Persistence: joblib (model + scaler saved for real-time use)
- Environment: Google Colab, Jupyter Notebook

---

## 🚀 Quick Start

git clone https://github.com/sachumonpsajeev-cyber/Physiological-Signal-Based-Stress-Prediction
cd Physiological-Signal-Based-Stress-Prediction
pip install pandas numpy scikit-learn joblib
jupyter notebook ML_Sachu_Project.ipynb

Open in Colab: https://colab.research.google.com/drive/1kuCQ2WMZpqF4GvftbvkDN87gB8h7wru?usp=sharing

---

## 👤 Author

Sachu Mon Puthenpuraickpal Sajeev
MSc Data Science & AI — TSI University, Riga, Latvia
LinkedIn: https://linkedin.com/in/sachu-mon
GitHub: https://github.com/sachumonpsajeev-cyber
whatsapp:+371-22447242
