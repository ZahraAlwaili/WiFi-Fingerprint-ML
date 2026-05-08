# DeepLocate-UJI: High-Precision Indoor Positioning via WiFi Fingerprinting

This repository contains a comprehensive machine learning system developed for the **DSAI 3201 Machine Learning Project**. [cite_start]The system predicts a user’s precise location (building, floor, and UTM coordinates) within a multi-building university campus using only WiFi Received Signal Strength Indicator (RSSI) data[cite: 9, 21].

## 📌 Project Overview
[cite_start]Indoor environments render GPS unreliable due to signal obstruction from walls and structural materials[cite: 24]. [cite_start]This project leverages the **UCI Indoor Localization WiFi Dataset**—a collection of 19,937 training samples and 1,111 validation samples—to build a cascaded positioning system that solves both classification and regression tasks[cite: 10, 31].

### **Key Metrics & Results**
* [cite_start]**Building Classification:** 100% Accuracy using Logistic Regression[cite: 13, 105].
* [cite_start]**Floor Classification:** 87.76% Accuracy using a Multi-Layer Perceptron (MLP)[cite: 13, 93].
* [cite_start]**Coordinate Regression:** R² of 0.9541 and an RMSE of 19.95 meters using XGBoost[cite: 13, 129].

---

## 🏗️ System Architecture
[cite_start]The localization problem is decomposed into a hierarchical pipeline to narrow down user location from macro (building) to micro (coordinates)[cite: 31, 165]:

| Task | Goal | Model Used |
| :--- | :--- | :--- |
| **Building Classification** | [cite_start]Identify which of the 3 campus buildings the user is in[cite: 31]. | [cite_start]Logistic Regression [cite: 102] |
| **Floor Classification** | [cite_start]Determine the specific floor level (0–4)[cite: 31]. | [cite_start]MLP Neural Network [cite: 88] |
| **Coordinate Regression** | [cite_start]Estimate exact UTM Longitude and Latitude[cite: 31]. | [cite_start]XGBoost / MLP Regressor [cite: 79, 107] |

---

## 🛠️ Data Preprocessing
* [cite_start]**No-Signal Encoding:** Replaced the sentinel value of 100 with **-105 dBm** to represent a logical gap between weak signals and complete absence[cite: 56, 169].
* [cite_start]**Feature Scaling:** Applied `StandardScaler` to ensure WAP features and coordinate targets were weighted equally during training[cite: 60, 109].
* [cite_start]**Handling Sparsity:** Managed a **96.5% sparsity rate**, where fingerprints typically only contained 18 active access points out of 520[cite: 47, 159].

---

## 📂 Repository Structure
* `notebooks/`: Jupyter notebooks covering EDA, preprocessing, and model training.
* `presentation/`: Final project presentation slides (PDF).
* `reports/`: Individual EDA report and the Final Group Report.
* `data/`: Placeholder for the UCI dataset (see download instructions below).

---

## 🚀 Getting Started

### **1. Dataset**
[cite_start]The models are trained on the **UCI Indoor Localization WiFi Dataset**[cite: 36].
* **Download:** [UCI Dataset Link](https://archive.ics.uci.edu/ml/datasets/ubiquitous+communication+community+university+jaume+i+indoor+localization+database)
* Place `trainingData.csv` and `validationData.csv` into the `/data` folder.

### **2. Dependencies**
```bash
pip install scikit-learn xgboost pandas numpy matplotlib seaborn
