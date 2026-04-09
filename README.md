# 🫀 ECG Data-Based Blood Pressure Estimation

> Estimating Systolic (SBP) and Diastolic (DBP) Blood Pressure from ECG signals using Machine Learning — built for wearable and resource-constrained devices.

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python)
![ML](https://img.shields.io/badge/ML-AdaBoost%20%7C%20ANN-orange)
![Dataset](https://img.shields.io/badge/Dataset-MIMIC--II-green)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

---

## 📌 Overview

Blood pressure (BP) is a key indicator of cardiovascular health. Traditional BP monitoring is invasive or requires dedicated hardware. This project proposes a **non-invasive, ECG-only approach** to estimate BP using machine learning — making it suitable for integration into wearable devices.

The link between the electrical and mechanical activity of the heart, known as **Mechano-Electric Coupling (MEC)**, forms the theoretical foundation of this work.

**Authors:** Rishav Kumar (B19ME066) & Om Solanki (B19CSE061)  
**Mentor:** Dr. Binod Kumar

---

## 🎯 Problem Statement

Given raw ECG signal data, the goal is to:

1. **Estimate** Systolic Blood Pressure (SBP), Diastolic Blood Pressure (DBP), and Mean Arterial Pressure (MAP).
2. **Classify** the reading into one of three categories:

| Category | SBP (mm Hg) | | DBP (mm Hg) |
|---|---|---|---|
| Normal | ≤ 90 or 90–120 | OR / AND | ≤ 60 or 60–79 |
| Prehypertension | 120–140 | OR | 80–90 |
| Hypertension | ≥ 140 (various sub-ranges) | OR / AND | ≥ 90 (various sub-ranges) |

---

## 🗂️ Dataset

**MIMIC-II** (Multi-Parameter Intelligent Monitoring in Intensive Care) — open-source dataset from [PhysioNet](https://physionet.org/).

- **942 ICU patients**, data collected between 2001–2008
- Sampling rate: **125 Hz**
- Signals: Aorta Blood Pressure (ABP), ECG, Photoplethysmograph (PPG)
- Pre-filtered to remove discontinuities and abnormal heart rate readings
- No patient demographic data (age, sex) included

---

## ⚙️ Methodology

### Pipeline

```
Raw ECG (125 Hz)
      │
      ▼
4-second segmentation (array length: 500)
      │
      ▼
2nd-order Bandpass Butterworth Filter (0.1–50 Hz)
      │
      ▼
R-peak Detection (neurokit2)  →  Remove segments with < 4 R-peaks
      │
      ▼
Clip to 4 consecutive R-peaks  →  Resample to 120 samples (via FFT)
      │
      ▼
Feature Extraction + (Optional) Classification
      │
      ▼
Regression (AdaBoost / ANN)
      │
      ▼
SBP, DBP, MAP
```

### Method 1 — Direct Regression

Train regressors directly on pre-processed ECG data.

- **1a:** Use all preprocessed data (non-uniform R-peak spacing)
- **1b:** Filter out samples with irregular R-peak intervals (±10% tolerance) for uniform spacing

**Models used:**
- AdaBoost Regressor (K-Fold CV, K=5; train-test split: 67/33)
- ANN Regressor — 3 hidden layers (1024 → 512 → 64 neurons), ReLU activation, Adam optimizer (lr=0.01), Dropout (0.5, 0.5, 0.25), 100 epochs

### Method 2 — Classify Then Regress

1. Classify ECG segment into Normal / Prehypertension / Hypertension using an **XGBoost classifier** (built by a separate team)
2. Route the segment to the corresponding class-specific regression model
3. Predict SBP and DBP using ANN or AdaBoost

---

## 📊 Results

### Method 1

| Data Type | Regressor | RMSE (SBP) | RMSE (DBP) |
|---|---|---|---|
| Non-Uniform | AdaBoost | 19.71 | 21.57 |
| Non-Uniform | ANN | 15.19 | 9.10 |
| Uniform | AdaBoost | 19.67 | 14.27 |
| **Uniform** | **ANN** | **12.76** | **6.34** |

### Method 2 (ANN, per class)

| Class | RMSE (SBP) | RMSE (DBP) |
|---|---|---|
| Normal | 12.47 | 4.68 |
| Prehypertension | 10.75 | 8.13 |
| Hypertension | 11.19 | 8.86 |

> ✅ **Method 2 with ANN yields the best overall performance**, particularly for DBP in the Normal class (RMSE: 4.68 mm Hg).

---

## 🧠 Model Architecture (ANN)

```
Input Layer  →  1024 neurons (ReLU) + Dropout(0.5)
             →  512  neurons (ReLU) + Dropout(0.5)
             →  64   neurons (ReLU) + Dropout(0.25)
Output Layer →  1 neuron (Linear) — predicts SBP or DBP
```

- Optimizer: Adam (lr = 0.01)
- Loss: MSE
- Epochs: 100
- Separate models trained for SBP and DBP

---

## 📈 Key Takeaways

- **ANN outperforms AdaBoost** across nearly all configurations.
- **Uniform R-peak spacing** (±10% filtering) improves model accuracy.
- **Classify-then-regress (Method 2)** consistently beats direct regression, especially for DBP.
- The approach is well-suited for **wearable devices** — no PPG or invasive sensors required.

---

## 📚 References

1. [ECG-Based BP Estimation — ArXiv](https://arxiv.org/ftp/arxiv/papers/2008/2008.10099.pdf)
2. [Blood Pressure Dataset — Kaggle](https://www.kaggle.com/datasets/mkachuee/BloodPressureDataset/discussion)
3. [Blood Pressure Analysis Notebook — Kaggle](https://www.kaggle.com/code/stephenmugisha/bloodpressure-analysis)
4. Banerjee, S., Kumar, B., & Tripathi, J. N. — *Blood Pressure Estimation from ECG Data Using XGBoost and ANN for Wearable Devices*, IEEE.
5. Mousavi, S. S., et al. — *ECG-Based Blood Pressure Estimation Using Mechano-Electric Coupling Concept*.
6. [ANN Regression with TensorFlow — Analytics Vidhya](https://www.analyticsvidhya.com/blog/2021/08/a-walk-through-of-regression-analysis-using-artificial-neural-networks-in-tensorflow/)

---

## 📄 License

This project is for academic purposes. Please cite appropriately if you use this work.
