# ECG Data Based Blood Pressure Prediction

A machine learning project that predicts **blood pressure (systolic and diastolic)** using **ECG (Electrocardiogram) signals**.  
The goal of this project is to explore the feasibility of **non-invasive and cuff-less blood pressure estimation** using biomedical signal processing and machine learning techniques.

---

## 📌 Project Overview

Traditional blood pressure measurement requires a cuff-based device. This project explores a **data-driven approach to estimate blood pressure directly from ECG signals**.

The system processes ECG waveform data, extracts meaningful physiological features, and trains machine learning models to predict blood pressure values.

The pipeline includes:

1. ECG signal preprocessing
2. Feature extraction from waveform patterns
3. Machine learning model training
4. Prediction and evaluation

---

## 🚀 Key Features

- Processed and analyzed **thousands of ECG signal samples**
- Implemented **signal preprocessing techniques** including filtering, normalization, and segmentation
- Extracted **multiple physiological features** from ECG waveforms
- Built a **machine learning regression model** for blood pressure estimation
- Achieved **~85–90% correlation between predicted and actual BP values**
- Improved model performance through **feature engineering and hyperparameter tuning**
- Implemented **data visualization for ECG signals and prediction analysis**

---

## 🏗 System Architecture

```
ECG Data
   │
   ▼
Signal Preprocessing
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

## 🧠 Technologies Used

| Technology | Purpose |
|------------|--------|
| **Python** | Core programming language |
| **NumPy** | Numerical computations |
| **Pandas** | Data manipulation and analysis |
| **Scikit-learn** | Machine learning models and evaluation |
| **SciPy** | Signal processing utilities |
| **Matplotlib / Seaborn** | Data visualization |
| **Jupyter Notebook** | Experimentation and model development |

---

## 📊 Machine Learning Workflow

### 1️⃣ Data Preprocessing
- Noise removal and signal filtering
- ECG waveform normalization
- Segmentation of ECG signals

### 2️⃣ Feature Extraction
Extracted ECG-based features such as:

- R-peak detection
- RR intervals
- Temporal waveform intervals
- Signal morphology characteristics

### 3️⃣ Model Training
Regression-based machine learning models were trained to predict:

- **Systolic Blood Pressure**
- **Diastolic Blood Pressure**

### 4️⃣ Model Evaluation
Evaluation metrics included:

- Mean Absolute Error (MAE)
- Mean Squared Error (MSE)
- Correlation between predicted and actual BP values

---

## 📈 Results

| Metric | Result |
|------|------|
| Prediction Accuracy | ~85–90% correlation |
| Dataset Size | Thousands of ECG samples |
| Model Type | Regression-based ML |

The results demonstrate the potential of **ECG-based BP prediction for future wearable healthcare monitoring systems**.

---

## 📂 Project Structure

```
ECG-data-based-BP-Prediction
│
├── data/
│   ├── raw_ecg_data
│   └── processed_data
│
├── notebooks/
│   └── model_training.ipynb
│
├── src/
│   ├── preprocessing.py
│   ├── feature_extraction.py
│   ├── model_training.py
│   └── evaluation.py
│
├── results/
│   ├── graphs
│   └── model_outputs
│
├── requirements.txt
└── README.md
```

---

## ⚙️ Installation

Clone the repository:

```bash
git clone https://github.com/itsomsolanki/ECG-data-based-BP-Prediction.git
```

Navigate to the project directory:

```bash
cd ECG-data-based-BP-Prediction
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## ▶️ Running the Project

Run the training pipeline:

```bash
python src/model_training.py
```

Or open the Jupyter notebook:

```bash
jupyter notebook
```

---

## 📊 Example Visualization

The project includes visualizations for:

- ECG waveform patterns
- Feature distributions
- Prediction vs actual BP comparison
- Model performance metrics

---

## 🔬 Future Improvements

- Deep learning models (CNN / LSTM for ECG signal processing)
- Larger biomedical datasets
- Real-time prediction using wearable device signals
- Integration with healthcare monitoring systems

---

GitHub:  
https://github.com/itsomsolanki

---
