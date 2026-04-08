# 📉 Robustness of Retail Forecasting Models Under Data Corruption

> Models that perform best on clean data are NOT the most reliable in production.

This project shows that while deep learning models achieve the lowest error on clean retail data, **Random Forest outperforms all models under real-world noise**, and a simple noise-aware training strategy improves robustness by **+40.88%**.

## ⚡ TL;DR

- 🥇 **Best Accuracy (Clean Data):** MLP (~5.5% MAPE)
- 🛡️ **Most Robust Model:** Random Forest
- 📉 **Biggest Failure:** MLP under noise (~3–4x degradation)
- 🚀 **Key Result:** Noise-aware training improved robustness by **+40.88%**

## 🌍 Why This Matters

In real-world retail systems:
- Data is often incomplete, noisy, or incorrect
- Models are rarely retrained instantly
- Small errors can lead to large inventory or revenue losses

👉 This project demonstrates that **robustness > raw accuracy** in production systems.

## Project Overview
In retail, data is rarely pristine. It is often plagued by missing values, sensor noise, and manual entry errors. This project benchmarks ARIMA, Prophet, Random Forest, XGBoost, and MLP models to determine which architectures are most resilient to data degradation and introduces a "Noise-Aware" training strategy to mitigate performance loss.

## Dataset and Features
The analysis used a retail sales dataset of 70,000 transactions spanning 2018–2022.
* Categories: Electronics, Groceries, Clothing, Sports.
* Key Features: Unit Price, Units Sold, Revenue, Discounts, and Holiday Flags.
* Preprocessing: Validated revenue calculations and handled temporal alignment.

## Experimental Methodology
The experiment was conducted in three distinct phases:

1. Baseline Training: All models were trained on 100% clean data to establish maximum potential accuracy.
2. Controlled Corruption: I injected synthetic noise and feature-level corruption into the test set to simulate real-world failure points.
3. Noise-Aware Training: I retrained the top-performing ML model (Random Forest) using a mix of clean and corrupted data to teach the model to ignore inconsistencies.

## Performance and Robustness Results


The table below compares the Mean Absolute Percentage Error (MAPE) of the models under different conditions.


![Status](https://img.shields.io/badge/status-complete-brightgreen)
![Models](https://img.shields.io/badge/models-5-blue)
![Metric](https://img.shields.io/badge/metric-MAPE-orange)

### 🔍 Results Overview

## 📊 Model Performance Ranking

Based on overall performance (accuracy on clean data + robustness to corrupted data), the models are ranked as follows:

### 🏆 Best to Worst

1. **Random Forest**
   - Clean Data (MAPE): ~5.7%
   - Corrupted Data (MAPE): ~8–11%
   - Robustness: 🟢 High  
   - ✅ Best overall balance of accuracy and robustness

2. **XGBoost**
   - Clean Data (MAPE): ~5.6%
   - Corrupted Data (MAPE): ~12–15%
   - Robustness: 🟡 Moderate  
   - ⚖️ Strong performance but less robust than Random Forest

3. **MLP (Neural Network)**
   - Clean Data (MAPE): ~5.5%
   - Corrupted Data (MAPE): ~18–25%
   - Robustness: 🔴 Low  
   - ⚠️ Excellent on clean data, but degrades significantly with noise

4. **ARIMA**
   - Clean Data (MAPE): 15.9%
   - Corrupted Data (MAPE): N/A
   - Robustness: 🔴 Low  
   - 📉 Traditional model with lower accuracy

5. **Prophet**
   - Clean Data (MAPE): 16.2%
   - Corrupted Data (MAPE): N/A
   - Robustness: 🔴 Low  
   - 📉 Lowest overall performance in this comparison

---

### 💡 Key Takeaways

- **Best for real-world (noisy) data:** Random Forest  
- **Best for clean data only:** MLP / XGBoost  
- **Most consistent model:** Random Forest  
- **Least reliable overall:** Prophet



### ⚠️ Notes

> Corruption experiments were only applied to tabular machine learning models  
> (XGBoost, MLP, Random Forest).  
> ARIMA and Prophet were evaluated on clean data only.

---

### 📌 Interpretation Guide

- 🔴 **Low Robustness** → Performance drops significantly with noisy data  
- 🟡 **Moderate Robustness** → Some degradation, but still usable  
- 🟢 **High Robustness** → Stable even under data corruption  

### The Noise-Aware Breakthrough
While the MLP was the most precise on clean data, it was brittle. The Random Forest showed the best natural resilience. By applying Noise-Aware training to the Random Forest, I achieved a significant jump in reliability:

| Metric | Original RF | Noise-Aware RF | Improvement |
| :--- | :---: | :---: | :---: |
| Robustness Score | 57.92% | 98.80% | +40.88% |

---

### **Key Observations**
* **Best Overall Performance:** While **MLP** slightly edges out the competition on clean data, **Random Forest** shows significantly better robustness when dealing with corrupted data.
* **Model Sensitivity:** The **MLP** model's error more than doubles (from 11.5 to 29.8) when moving from clean to corrupted data, whereas **Random Forest** actually reports a lower MAPE in the corrupted set provided.
* **Outliers:** The **ARIMA / Prophet** models performed significantly worse than all other candidates across both datasets, suggesting they may not be suitable for this specific time-series or data structure.


## Technologies Used
* Modeling: Scikit-learn, XGBoost, TensorFlow (Keras), Prophet, Statsmodels.
* Data Science: Pandas, NumPy, Matplotlib.
* Environment: Jupyter Notebook / Python 3.x.
