# ECG Data-Based Blood Pressure Estimation

A machine learning project that estimates **Systolic Blood Pressure (SBP)** and **Diastolic Blood Pressure (DBP)** using **Electrocardiogram (ECG) signals**.  
The project explores the **Mechano-Electric Coupling (MEC)** relationship between the electrical activity of the heart (ECG) and the mechanical activity responsible for blood pressure.

This approach enables **non-invasive blood pressure estimation** and can be integrated into **wearable healthcare monitoring devices**.

---

## 📌 Project Overview

Blood pressure is traditionally measured using cuff-based devices. However, continuous monitoring using such methods is inconvenient.

This project proposes a **machine learning-based solution** that estimates blood pressure using **only ECG signals**, enabling potential integration with wearable ECG devices.

The system performs:

1. ECG signal preprocessing
2. Feature extraction using R-peak detection
3. Machine learning regression for BP prediction
4. Classification into BP categories

---

## 🎯 Objectives

- Predict **Systolic Blood Pressure (SBP)** and **Diastolic Blood Pressure (DBP)** using ECG signals
- Classify BP readings into:
  - Normal
  - Prehypertension
  - Hypertension
- Develop a **low-computation ML pipeline suitable for wearable devices**

---

## 📊 Dataset

The project uses the **MIMIC-II Waveform Dataset** from PhysioNet.

Key characteristics:

- Signals from **942 ICU patients**
- Data collected between **2001–2008**
- Sampling frequency: **125 Hz**
- Includes synchronized:
  - ECG signals
  - Arterial Blood Pressure (ABP)
  - Photoplethysmograph (PPG)

Signal segments with abnormal heart rates or discontinuities were removed to ensure data quality.

---

## ⚙️ Methodology

### 1️⃣ Data Preprocessing

- ECG signals divided into **4-second segments (500 samples)**
- Applied **2nd-order Butterworth Bandpass Filter (0.1–50 Hz)** to remove noise
- Detected **R-peaks using NeuroKit2 library**
- Segments with fewer than **4 R-peaks** were discarded

---

### 2️⃣ Signal Processing

- Extracted ECG signals between **four consecutive R-peaks**
- Segment lengths varied between **117–450 samples**
- Used **FFT-based resampling** to normalize signal length to **120 samples**

---

### 3️⃣ Machine Learning Models

Two regression models were implemented:

#### AdaBoost Regressor
- Ensemble-based regression model
- Uses multiple weak estimators (Decision Trees)
- Improves prediction accuracy through boosting

#### Artificial Neural Network (ANN)

Architecture:

Input Layer  
Hidden Layer 1 – **1024 neurons**  
Hidden Layer 2 – **512 neurons**  
Hidden Layer 3 – **64 neurons**

Additional details:

- Activation: **ReLU**
- Optimizer: **Adam**
- Learning Rate: **0.01**
- Dropout: **0.5 / 0.5 / 0.25**
- Training epochs: **100**

---

## 🧠 Approaches Implemented

### Method 1 – Direct Regression

- Train models directly on ECG features
- Predict SBP and DBP values

Two dataset variations:

1. **Non-uniform R-peak spacing**
2. **Uniform R-peak spacing (±10% threshold filtering)**

---

### Method 2 – Classification + Regression

1. First classify BP category:
   - Normal
   - Prehypertension
   - Hypertension

2. Apply regression models separately for each class to predict SBP and DBP.

This approach achieved **lower prediction error**.

---

## 📈 Results

### Method 1 Results

| Model | RMSE SBP | RMSE DBP |
|------|------|------|
| AdaBoost | 19.70 | 21.57 |
| ANN | 15.18 | 9.09 |
| ANN (Uniform Data) | **12.75** | **6.33** |

---

### Method 2 Results (Best Results)

| Class | Model | RMSE SBP | RMSE DBP |
|------|------|------|------|
| Normal | ANN | 12.46 | 4.67 |
| Prehypertension | ANN | 10.74 | 8.13 |
| Hypertension | ANN | 11.18 | 8.85 |

The **classification + regression pipeline produced lower prediction errors** compared to direct regression.

---

## 🧠 Technologies Used

| Technology | Purpose |
|------------|--------|
| Python | Core programming language |
| NumPy | Numerical computing |
| Pandas | Data processing |
| Scikit-learn | Machine learning models |
| TensorFlow / Keras | ANN implementation |
| NeuroKit2 | ECG signal processing |
| SciPy | Signal filtering |
| Matplotlib | Visualization |
| FFT | Signal resampling |

---

## 🏗 Project Workflow

```
ECG Signal
   │
   ▼
Signal Preprocessing (Filtering)
   │
   ▼
R-Peak Detection
   │
   ▼
Signal Segmentation
   │
   ▼
Feature Extraction
   │
   ▼
Machine Learning Model
   │
   ▼
Blood Pressure Prediction
```

---

## 🔬 Future Improvements

- Use **Deep Learning models (CNN / LSTM)** for ECG signal processing
- Deploy the model on **edge devices or wearable health monitors**
- Use larger biomedical datasets for improved generalization
- Integrate **real-time BP monitoring applications**

---

## 📚 References

1. PhysioNet MIMIC-II Dataset  
2. Blood Pressure Estimation using ML (Research Papers)  
3. ECG-Based Blood Pressure Estimation using Mechano-Electric Coupling  

