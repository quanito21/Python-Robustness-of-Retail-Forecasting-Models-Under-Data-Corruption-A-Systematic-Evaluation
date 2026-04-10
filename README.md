# 📉 Robustness of Retail Forecasting Models Under Data Corruption

> Models that perform best on clean data are NOT always the most reliable in production.

This project shows that while deep learning models (LSTM) achieve the lowest error on clean retail data, **Ensemble models (XGBoost/Random Forest) outperform them under real-world noise**, and a noise-aware training strategy improves robustness by **+36.91%**.

## 🌍 Why This Matters

In real-world retail systems:
- Data is often incomplete, noisy, or incorrect.
- Models are rarely retrained instantly.
- Small errors can lead to large inventory or revenue losses.

👉 This project demonstrates that **robustness > raw accuracy** for production reliability.

## Project Overview
In retail, data is rarely pristine. It is often plagued by missing values, sensor noise, and manual entry errors. This project benchmarks ARIMA, Random Forest, XGBoost, and LSTM models to determine which architectures are most resilient to data degradation and introduces a "Noise-Aware" training strategy to mitigate performance loss.

## Dataset and Features
The analysis used a retail sales dataset of 70,000 transactions spanning 2018–2022.
* **Categories:** Electronics, Groceries, Clothing, Sports.
* **Key Features:** Unit Price, Units Sold, Revenue, Discounts, and Holiday Flags.
* **Preprocessing:** Validated revenue calculations and handled temporal alignment.

## Experimental Methodology
1. **Baseline Training:** All models were trained on 100% clean data to establish maximum potential accuracy.
2. **Controlled Corruption:** I injected synthetic noise and feature-level corruption into the test set to simulate real-world failure points.
3. **Noise-Aware Training:** I retrained the Random Forest using a mix of clean and corrupted data to teach the model to ignore inconsistencies.

# 🔍 Results & Performance Metrics

### 🏆 Model Rankings: Reliability vs. Precision

| Rank | Model | MAPE (Clean) | MAPE (Dirty) | Robustness Score | Status |
| :--- | :--- | :---: | :---: | :---: | :--- |
| **1** | **XGBoost** | 1.48% | 2.28% | **64.91%** | 🏆 **Top Pick** |
| **2** | **Random Forest** | 1.51% | 2.44% | **61.89%** | 🟢 **Stable** |
| **3** | **LSTM** | 1.32% | 2.92% | **45.21%** | 🟡 **Brittle** |
| **4** | **ARIMA** | >20.0% | >25.0% | **Low** | 🔴 **Unreliable** |

---

### ⚡ The "Noise-Aware" Breakthrough
By applying **Noise-Aware Training** to the Random Forest, I achieved a near-perfect resilience score, effectively "teaching" the model to handle corruption.

| Strategy | Robustness Score | Improvement |
| :--- | :---: | :---: |
| **Standard Random Forest** | 61.89% | -- |
| **Noise-Aware Random Forest** | **98.80%** | **+36.91%** |

---

🏆 Model Rankings: Reliability vs. Precision after Noise-Aware

| Rank | Model                     | MAPE (Clean) | MAPE (Dirty) | Robustness Score | Status            |
|------|---------------------------|--------------|--------------|------------------|-------------------|
| 1    | Noise-Aware Random Forest | 1.51%        | 1.53%        | 98.80%           | 🏆 Elite Stability |
| 2    | XGBoost                   | 1.48%        | 2.28%        | 64.91%           | 🟢 Top Pick        |
| 3    | Random Forest (Standard)  | 1.51%        | 2.44%        | 61.89%           | 🟢 Stable          |
| 4    | LSTM                      | 1.32%        | 2.92%        | 45.21%           | 🟡 Brittle         |
| 5    | ARIMA                     | >20.0%       | >25.0%       | Low              | 🔴 Unreliable      |


### 💡 Key Takeaways

* **Accuracy vs. Robustness:** The **LSTM** was the most precise on clean data (1.32% MAPE) but the most fragile, with its error increasing by over 120% under noise.
* **Ensemble Resilience:** **XGBoost** and **Random Forest** proved more reliable because their tree-based structures naturally average out localized noise.
* **The Winner:** For real-world deployment, the **Noise-Aware Random Forest** is the clear winner, offering near-total immunity to the simulated data corruptions.

### **Key Observations**
* **Model Sensitivity:** The LSTM model's dependency on sequential consistency makes it highly vulnerable to even small perturbations in input features.
* **Outliers:** **ARIMA** performed significantly worse (>20% MAPE) even on clean data, suggesting it cannot capture the non-linear complexities of this retail dataset.

## Technologies Used
* **Modeling:** Scikit-learn, XGBoost, TensorFlow (Keras), Statsmodels.
* **Data Science:** Pandas, NumPy, Matplotlib.
* **Environment:** Jupyter Notebook / Python 3.x.
