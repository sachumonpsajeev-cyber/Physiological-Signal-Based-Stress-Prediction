# Physiological-Signal-Based-Stress-Prediction
The main goal of the project was to develop a system capable of handling raw physiological data, identifying the features to extract, training the models used to classify data, assessing their effectiveness, and, ultimately, to come up with a way of predicting the stress level in real time
# Physiological Signal – Based Stress Prediction

## Table of Contents
1. [Introduction](#1-introduction)
2. [Phase 1: Data Loading and Initial Inspection](#2-phase-1-data-loading-and-initial-inspection)
3. [Phase 2: Data Preprocessing](#3-phase-2-data-preprocessing)
4. [Phase 3: Feature Engineering (Windowing)](#4-phase-3-feature-engineering-windowing)
5. [Phase 4: Model Training and Assessment](#5-phase-4-model-training-and-assessment)
6. [Phase 5: Analysis and Saving of Models](#6-phase-5-analysis-and-saving-of-models)
7. [Phase 6 & 7: Prediction System in Real-Time](#7-phase-6--7-prediction-system-in-real-time)
8. [Phase 8: Final Report and Graphical Representation](#8-phase-8-final-report-and-graphical-representation)
9. [Conclusion](#9-conclusion)
10. [Bibliography](#10-bibliography)

---

## 1. Introduction

This report outlines the creation of a machine learning model in order to predict stress using physiological indicators. The main goal of the project was to develop a system capable of handling raw physiological data, identifying the features to extract, training the models used to classify data, assessing their effectiveness, and, ultimately, to come up with a way of predicting the stress level in real time. The project was based on the multi-phase approach, which included the first data inspection and extends to the deployment and analysis of the model.

---

## 2. Phase 1: Data Loading and Initial Inspection

The project has started by loading the `Physiologicalsignals60sn.csv` dataset. The first examination showed the following:

- **Shape of Dataset:** 168,000 rows in the beginning, 10 columns.
- **Types of Data:** There were columns of `float64` (e.g., eda, bvp, temp) and `int64` (e.g., x, y, z motion sensors, stress indication). There was an object type column (`Unnamed: 9`).
- **Missing Values:** There were large missing values in `Unnamed: 7` (100%), `Unnamed: 8` (100%), and `Unnamed: 9` (almost 100%).
- **Duplicates:** 28,808 rows were found repeated or duplicate entries.
- **Target Variable:** The major target variable was found to be the `stress indication` column, which represented various levels of stress.
- **Correlation Matrix:** Correlation Matrix was calculated when the columns were numeric in nature and showed the relationship between the physiological signals.
- **Distributions:** Plots of histograms were made of numeric columns to show their distributions.
- **Numbers of Values:** Counts of values were presented in categorical columns (although only in relation to the column with the name `Unnamed`).

This step was important in offering important information about data quality and characteristics that could be used in the further preprocessing.

---

## 3. Phase 2: Data Preprocessing

The crude data was preprocessed in a few stages leading to its use in training the models:

- **Duplicate Removal:** 28,809 duplicate rows were eliminated in the dataset, which guarantees that there were no duplicates in the data set.
- **Name Cleaning of Columns:** All column names were made clean of whitespace.
- **Irrelevant Column Dropping:** Columns that were found to be largely empty or were termed Unnamed (`Unnamed: 7`, `Unnamed: 8`, `Unnamed: 9`) have been dropped because no meaningful data was present in them or they were all-null. This was a very important aspect of eliminating noise.
- **Target Identification:** It was clearly identified that the target variable was the `stress indication` column.
- **Missing Value Imputation:**
  - Numeric columns: The missing values were filled with the median value of each column.
  - Categorical columns: The missing values were filled in with the mode of the respective columns. There were no categorical columns left after the removal of the `Unnamed` columns in this particular run.
- **Numerical Feature Scaling:** `StandardScaler` was used to scale all the numeric feature columns (except the target column of `stress indication`). This standardization ensures features have the same contribution to the training process of the model. The trained StandardScaler was saved as `scaler.joblib` for future real-time predictions.
- **Categorical Feature Encoding:** No categorical features were left behind following the earlier cleaning processes and, therefore, no encoding was carried out.

After preprocessing, the dataset was cleaned, normalized and ready for feature engineering.

---

## 4. Phase 3: Feature Engineering (Windowing)

To capture dynamic patterns in physiological signals, a windowing approach was employed to extract time-domain and frequency-domain features. The configuration used was:

- **Window Size:** 5 data points per window.
- **Step Size:** 2 data points (resulting in overlapping windows).

The signal columns used for feature extraction were: `eda(electrodermal-activity)`, `bvp(blood volume pressure)`, `temp`, `x(horizontal motion)`, `y(vertical motion)`, and `z(depth axis)`.

For each window and each signal column, the following features were calculated:

**Time-Domain Features:**
| Feature | Description |
|---|---|
| Mean | Average value |
| Std | Standard Deviation |
| Min | Minimum value |
| Max | Maximum value |
| Median | Median value |
| RMS | Root Mean Square |
| Skew | Skewness |
| Kurtosis | Kurtosis |

**Frequency-Domain Features:**
| Feature | Description |
|---|---|
| dom_freq | Dominant Frequency |
| spec_entropy | Spectral Entropy |

The mode (most frequent value) of the `stress indication` of each window was used to determine the target variable. The resulting feature data assumed the shape of **(69,594 × 61)** — 69,594 windows with 60 features each, plus the target column.

---

## 5. Phase 4: Model Training and Assessment

The extracted features were trained and evaluated on several machine learning models. The dataset was split into training (80%) and testing (20%) sets, resulting in **55,675 training** and **13,919 testing** samples.

Three classification models were trained and tested:

- Random Forest Classifier
- Decision Tree Classifier
- Logistic Regression

### Model Comparison

| Model | Accuracy | Precision | Recall | F1 Score |
|---|---|---|---|---|
| **Random Forest** | **0.9592** | **0.9595** | **0.9592** | **0.9589** |
| Decision Tree | 0.9248 | 0.9247 | 0.9248 | 0.9247 |
| Logistic Regression | 0.6526 | 0.6134 | 0.6526 | 0.5670 |

> ✅ **Best performing model: Random Forest**

### Classification Report – Random Forest

| Class | Precision | Recall | F1-Score | Support |
|---|---|---|---|---|
| 0 | 0.95 | 0.98 | 0.97 | 9028 |
| 1 | 0.97 | 0.91 | 0.94 | 4840 |
| 2 | 1.00 | 0.96 | 0.98 | 51 |
| **Weighted Avg** | **0.96** | **0.96** | **0.96** | **13919** |

The evaluation of models was based on Accuracy, Precision, Recall, and F1-Score (weighted average for multi-class classification).

---

## 6. Phase 5: Analysis and Saving of Models

This stage involved further analysis of the trained models and their persistence:

- **Confusion Matrices:** Confusion matrices were created for each model, illustrating their performance in classifying the various levels of stress.
- **Feature Importance:** The top 20 feature importances of tree-based models (Random Forest and Decision Tree) were plotted, revealing which engineered features were most influential in predicting stress and which physiological indicators were most applicable for stress detection.
- **Model Saving:** All trained models (Random Forest, Decision Tree, Logistic Regression) were stored as `.joblib` files (e.g., `RandomForestmodel.joblib`), which can subsequently be loaded and used without retraining.

---

## 7. Phase 6 & 7: Prediction System in Real-Time

A stress prediction system was created for incoming new physiological data:

- **Model and Scaler Loading:** `joblib` was used to load the best performing model (Random Forest) and the pre-fitted `StandardScaler`.
- **`preprocess_newdata` Function:** Repeats the preprocessing steps of Phase 2 on any new input DataFrame to ensure consistency in data transformation:
  - Eliminates whitespace in column names
  - Drops `Unnamed` or mostly-empty columns
  - Imputes missing values (numeric → median, categorical → mode)
  - Normalizes numerical features with the loaded `StandardScaler`
- **`predictstress` Function:** Receives incoming raw physiological measurements, performs preprocessing, applies the same windowing and feature extraction logic as Phase 3, then predicts stress levels using the loaded model. An overall prediction for the entire data segment is obtained via a **majority vote** of individual window predictions.

A demonstration confirmed the system's ability to load a new `physiologicalsignals60sn.csv` dataset and successfully predict a stress level (e.g., `0`) for the new data.

---

## 8. Phase 8: Final Report and Graphical Representation

The final stage consolidated the project results:

- **Model Performance Table:** A summary table of Accuracy, Precision, Recall, and F1-Score for all trained models.
- **Performance Visualization:** A bar chart comparing performance metrics across all models.
- **Best Model Confirmation:** The Random Forest Classifier was confirmed as the best overall performing model.

### Final Model Performance Summary

| Model | Accuracy | Precision | Recall | F1 Score |
|---|---|---|---|---|
| **Random Forest** | **0.9636** | **0.9636** | **0.9636** | **0.9635** |
| Decision Tree | 0.9327 | 0.9326 | 0.9327 | 0.9326 |
| Logistic Regression | 0.6599 | 0.6252 | 0.6599 | 0.5712 |

---

## 9. Conclusion

This project successfully established and tested a machine learning pipeline to predict stress using physiological data. The **Random Forest Classifier** achieved the best performance with a high F1-score of **0.96**. The developed pipeline — encompassing data preprocessing, windowing-based feature engineering, and an effective real-time prediction system — provides a solid foundation for implementing continuous stress monitoring in practical, real-life scenarios.

---

## 10. Bibliography

- Schmidt, P., Reiss, A., Duerichen, R., Maraneck, C., & Van Laerhoven, K. (2018). *Introducing WESAD, a Multimodal Dataset for Wearable Stress and Affect Detection.* Proceedings of the 20th ACM International Conference on Multimodal Interaction, 400–408.

- Abdelfattah, E., Joshi, S., & Tiwari, S. (2025). *Machine and Deep Learning Models for Stress Detection Using Multimodal Physiological Data.* IEEE Access, 13, 4597–4608. https://doi.org/10.1109/access.2024.3525459

- Lazarou, E., & Exarchos, T. P. (2024). *Predicting stress levels using physiological data: Real-time stress prediction models utilizing wearable devices.* AIMS Neuroscience, 11(1), 76–102. https://doi.org/10.3934/neuroscience.2024006

- Montesinos, V., Dell'Agnola, F., Arza, A., Aminifar, A., & Atienza, D. (2019). *MultiModal Acute Stress Recognition Using Off-the-Shelf Wearable Devices.* 2019 41st Annual International Conference of the IEEE Engineering in Medicine and Biology Society (EMBC). https://doi.org/10.1109/embc.2019.8857130

- Rashid, N., Mortlock, T., & Faruque, M. A. A. (2023). *Stress Detection using Context-Aware Sensor Fusion from Wearable Devices.* IEEE Xplore. https://doi.org/10.48550/arxiv.2303.08215

- Zhai, J., & Barreto, A. (2006). *Stress Detection in Computer Users Based on Digital Signal Processing of Noninvasive Physiological Variables.* Proceedings of the 28th Annual International Conference of the IEEE Engineering in Medicine and Biology Society.

- Kurniawan, H., Maslov, A. V., & Pechenizkiy, M. (2013). *Stress detection from speech and galvanic skin response (GSR).* IEEE International Conference on Multimedia and Expo Workshops (ICMEW).

---

## Links

- 📊 **Dataset:** [Google Sheets](https://docs.google.com/spreadsheets/d/1_txXosadFW3egV_fLzFScejxyzlPULBeVuHesAiDikI/edit?usp=sharing)
- 💻 **Code (Google Colab):** [Open Notebook](https://colab.research.google.com/drive/1kuCQ2WMZpqF4GvftbvkDN87gB8h7wru?usp=sharing)
