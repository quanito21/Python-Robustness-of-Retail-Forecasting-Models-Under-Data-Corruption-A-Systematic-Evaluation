# 📉 Robustness of Retail Forecasting Models Under Data Corruption

> Models that perform best on clean data are NOT the most reliable in production.

This project demonstrates that while deep learning models (LSTM) achieve the lowest error on clean retail data, **ensemble methods like Random Forest are significantly more robust under real-world data corruption**. By introducing a noise-aware training strategy, model robustness improved by **+40.88%**.

---

## ⚡ TL;DR

- 🥇 **Best Accuracy (Clean Data):** LSTM (RMSE ≈ 10.45)
- 🛡️ **Most Robust Model:** Random Forest
- 📉 **Biggest Failure:** LSTM under noise (largest RMSE increase)
- 🚀 **Key Result:** Noise-aware training improved robustness by **+40.88%**

---

## 🌍 Why This Matters

In real-world retail systems:
- Data is often noisy, incomplete, or misaligned  
- Forecasting models operate under imperfect conditions  
- Small prediction errors can lead to large inventory and revenue losses  

👉 This project shows that **robustness matters more than raw accuracy** in production forecasting systems.

---

## 🧠 Project Overview

This project evaluates forecasting models under **controlled data corruption** to better reflect real-world conditions.

A **Systematic Corruption Framework** was developed to simulate:
- Missing values  
- Label noise  
- Outliers  
- Temporal misalignment  

Models are evaluated not just on accuracy, but on how their performance **degrades as data quality worsens**.

---

## 📊 Dataset

- **70,000 retail transactions (2018–2022)**
- Categories: Electronics, Groceries, Clothing, Sports, Home & Kitchen  
- Features:
  - Unit Price  
  - Units Sold  
  - Revenue  
  - Discounts  
  - Holiday Flags  

✔ Clean dataset used as baseline before controlled corruption

---

## ⚙️ Methodology

### 1. Baseline Training
Train all models on clean data to establish maximum performance.

### 2. Controlled Corruption
Apply synthetic data issues:
- Missing values  
- Gaussian noise  
- Outliers  
- Time shifts  

### 3. Robustness Evaluation
Measure how model error increases under corruption.

### 4. Noise-Aware Training
Retrain Random Forest on corrupted data to improve stability.

---

## 📈 Results (RMSE-Based)

| Model            | RMSE (Clean) | RMSE (Corrupted) | Robustness |
|------------------|-------------|------------------|------------|
| **LSTM**          | **10.45**   | 23.10            | 🔴 Low      |
| **Random Forest** | 11.72       | 18.95            | 🟢 High     |
| **XGBoost**       | 11.55       | 17.80            | 🟡 Moderate |
| **ARIMA**         | 150+        | 170+             | 🔴 Low      |
| **Prophet**       | 150+        | 170+             | 🔴 Low      |

---

## 🚀 Noise-Aware Training Result

| Metric | Original RF | Noise-Aware RF | Improvement |
| :--- | :---: | :---: | :---: |
| Robustness Score | 57.92% | 98.80% | +40.88% |

👉 Training on corrupted data dramatically improved model stability without changing architecture.

---

## 🏆 Key Takeaways

- **Accuracy vs Robustness Tradeoff:**  
  LSTM achieves the best clean performance but is highly sensitive to noise  

- **Ensemble Advantage:**  
  Random Forest maintains stable performance under corruption  

- **Non-Linear Degradation:**  
  Models fail gradually at first, then collapse beyond a threshold  

- **Training Strategy Matters:**  
  Robustness can be improved without increasing model complexity  

---

## 🛠️ Technologies Used

- **Modeling:** Scikit-learn, XGBoost, TensorFlow (Keras), Prophet, Statsmodels  
- **Data Science:** Pandas, NumPy, Matplotlib  
- **Environment:** Jupyter Notebook / Python  
