# 🛡️ Intrusion Detection and Prevention System using CNN-LSTM

A deep learning-based **Network Intrusion Detection and Prevention System (NIDPS)** that combines Convolutional Neural Networks (CNN) and Long Short-Term Memory (LSTM) networks to detect and automatically respond to cyber attacks in real time.

---

## 📊 Results

| Metric | Score |
|--------|-------|
| **Accuracy** | 98.38% |
| **Precision** | 96.77% |
| **Recall** | 96.77% |
| **F1 Score** | 96.77% |

| | Predicted Negative | Predicted Positive |
|---|---|---|
| **Actual Negative** | 15,070 (TN) | 164 (FP) |
| **Actual Positive** | 164 (FN) | 4,914 (TP) |

### Performance Metrics
![Performance Metrics](results/Visual_representation_of_Performance_Metrics.jpg)

### Confusion Matrix
![Confusion Matrix](results/Confusion_Matrix.png)

### Sample Output
![Output Result](results/Output_Result.png)

---

## 🧠 Model Architecture

The model uses a hybrid **CNN + LSTM** architecture designed for sequential network traffic pattern analysis:

```
Input (10 selected features, reshaped to sequence)
    │
    ▼
Conv1D (32 filters, kernel_size=3, ReLU)
    │
    ▼
MaxPooling1D (pool_size=2)
    │
    ▼
LSTM (64 units)
    │
    ▼
Flatten
    │
    ▼
Dense (128, ReLU)
    │
    ▼
Dense (1, Sigmoid) → Binary classification
```

- **Optimizer:** Adam (lr=0.0001)
- **Loss:** Binary Crossentropy
- **Epochs:** 10 | **Batch size:** 32

---

## 🔍 Features

- **Preprocessing:** Handles infinite values, missing data, standard scaling, and one-hot encoding of IP addresses
- **Feature Selection:** SelectKBest (ANOVA F-test) selects top 10 most relevant features
- **Attack Detection:** Classifies network traffic as normal or malicious
- **Automated Response:** Takes action based on detected attack type:
  - 🔴 **DoS Attack** → Blocks source IP via `iptables`
  - 🟠 **Malware** → Quarantines the affected system
  - 🟡 **Port Scanning** → Blocks suspicious ports (1–1024)
  - 🟢 **Normal Traffic** → No action taken

---

## 📁 Project Structure

```
intrusion-detection-cnn-lstm/
├── CNN_LSTM.ipynb                  # Main notebook
├── requirements.txt                # Python dependencies
├── softwares.txt                   # Setup instructions
├── README.md
└── results/
    ├── Confusion_Matrix.png
    ├── Performance_metrics.png
    ├── Visual_Representation_of_Performance_Metrics.jpg
    └── Output_Result.png
```

---

## 📦 Dataset

This project uses the **SIMARGL2022** network traffic dataset.

- **Download:** [SIMARGL2022 on Kaggle](https://www.kaggle.com/datasets/h2020simargl/simargl2022)
- Place the CSV file at: `content/simargl2022_train4.csv` (if running in Google Colab)
- Target column: `ALERT` (attack type label)
- Source IP column: `IPV4_SRC_ADDR`

---

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- Google Colab (recommended) or local Jupyter environment

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/sreenidhivasireddy/intrusion-detection-cnn-lstm.git
   cd intrusion-detection-cnn-lstm
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Run the notebook**
   - Open `CNN_LSTM.ipynb` in [Google Colab](https://colab.research.google.com/) or Jupyter
   - Upload your dataset to `/content/simargl2022_train4.csv`
   - Run all cells sequentially

---

## 🛠️ Tech Stack

- **Language:** Python 3
- **Deep Learning:** TensorFlow / Keras
- **ML / Preprocessing:** scikit-learn
- **Data Handling:** pandas, NumPy
- **System Actions:** subprocess, iptables (Linux)
- **Environment:** Google Colab

---

## ⚠️ Notes

- The automated IP blocking and quarantine functions use Linux `iptables` and require `sudo` privileges. These are designed for Linux environments and will not run on Windows/macOS without modification.
- The prevention actions are meant as a **proof of concept** for automated incident response.

---

## 📄 License

This project is for academic and educational purposes.
