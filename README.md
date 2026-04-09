# ECG Data-Based Blood Pressure Prediction

A machine learning project that predicts **blood pressure (SBP and DBP)** directly from **ECG signals** using signal processing and regression models.  
The project explores a **non-invasive approach for blood pressure estimation**, which can potentially be integrated into **wearable healthcare monitoring systems**.

---

## 📌 Project Overview

Blood pressure monitoring traditionally requires cuff-based devices.  
This project investigates whether **ECG signals alone can be used to estimate blood pressure** by leveraging **machine learning models and biomedical signal processing techniques**.

The approach is based on the **Mechano-Electric Coupling (MEC)** concept, which links the electrical activity of the heart (ECG) with its mechanical activity responsible for blood pressure.

Using ECG waveform features and machine learning models, the system predicts:

- **Systolic Blood Pressure (SBP)**
- **Diastolic Blood Pressure (DBP)**

The predicted values can further be used to classify patients into:

- Normal
- Prehypertension
- Hypertension

---

## 🚀 Key Features

- Processed ECG signals from **900+ ICU patients** using the **MIMIC-II waveform dataset**
- Segmented ECG signals into **4-second windows (500 samples each)**
- Implemented **band-pass Butterworth filtering (0.1–50 Hz)** to remove noise
- Extracted **R-peak features** from ECG signals using **NeuroKit2**
- Developed regression models to predict **SBP and DBP**
- Achieved **RMSE as low as 12.75 (SBP) and 6.33 (DBP)** using ANN regression
- Applied **5-fold cross-validation** to evaluate model robustness

---

## 🧠 Technologies Used

| Technology | Purpose |
|------------|--------|
| **Python** | Core programming language |
| **NumPy** | Numerical computations |
| **Pandas** | Data processing and analysis |
| **Scikit-learn** | Machine learning models |
| **TensorFlow / Keras** | Artificial Neural Network implementation |
| **NeuroKit2** | ECG signal processing and R-peak detection |
| **SciPy** | Signal filtering and FFT |
| **Matplotlib / Seaborn** | Data visualization |
| **Jupyter Notebook** | Model experimentation |

---

## 🏗 Project Workflow

```
ECG Dataset
   │
   ▼
Signal Preprocessing
(Band-pass filtering)
   │
   ▼
Feature Extraction
(R-peak detection)
   │
   ▼
Dataset Segmentation
(4-second signal windows)
   │
   ▼
Machine Learning Models
(AdaBoost & ANN Regression)
   │
   ▼
SBP & DBP Prediction
```

---

## 📊 Dataset

The project uses the **MIMIC-II Waveform Dataset** containing:

- ECG signals
- Aortic Blood Pressure (ABP) signals
- Photoplethysmograph (PPG) signals

Dataset characteristics:

- **942 ICU patients**
- **125 Hz sampling rate**
- Thousands of ECG signal recordings

Each ECG signal segment is **filtered, normalized, and resampled before training the models**.

---

## ⚙️ Methodology

### 1️⃣ Data Preprocessing

- ECG signals divided into **4-second segments**
- Band-pass filtering using **Butterworth filter**
- Removal of noisy signals and irregular samples

---

### 2️⃣ Feature Extraction

- **R-peak detection** from ECG signals
- Distance between consecutive R-peaks
- ECG waveform segment analysis

Signals were resampled to **120 samples per segment** using **Fast Fourier Transform (FFT)**.

---

### 3️⃣ Machine Learning Models

Two models were implemented:

#### AdaBoost Regressor

Used for predicting SBP and DBP with ensemble learning.

Results:

| Metric | Value |
|------|------|
| RMSE (SBP) | ~19.66 |
| RMSE (DBP) | ~14.26 |

---

#### Artificial Neural Network (ANN)

Architecture:

- 3 Hidden Layers
- Neurons: **1024 → 512 → 64**
- Activation: **ReLU**
- Optimizer: **Adam**
- Epochs: **100**

Results:

| Metric | Value |
|------|------|
| RMSE (SBP) | ~12.75 |
| RMSE (DBP) | ~6.33 |

---

### 4️⃣ Classification + Regression Pipeline

The system also categorizes blood pressure into:

- **Normal**
- **Prehypertension**
- **Hypertension**

Separate regression models are trained for each category to improve prediction accuracy.

---

## 📈 Results

| Model | RMSE (SBP) | RMSE (DBP) |
|------|------------|------------|
| AdaBoost | ~19.66 | ~14.26 |
| ANN | ~12.75 | ~6.33 |

ANN regression showed **significantly lower prediction error** compared to AdaBoost.

---

## ▶️ Installation

Clone the repository:

```bash
git clone https://github.com/itsomsolanki/ECG-data-based-BP-Prediction.git
```

Navigate to the project folder:

```bash
cd ECG-data-based-BP-Prediction
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## ▶️ Running the Project

Run the model training pipeline:

```bash
python train_model.py
```

Or open the notebook:

```bash
jupyter notebook
```

---

## 📊 Visualizations

The project includes:

- ECG waveform visualization
- Filtered vs original ECG signals
- Training loss graphs
- Prediction vs actual BP comparison

---

## 🔬 Future Improvements

- Implement **deep learning models (CNN/LSTM) for ECG signal learning**
- Improve performance with **larger datasets**
- Deploy the model for **real-time wearable device monitoring**
- Build a **web interface for medical visualization**

---
