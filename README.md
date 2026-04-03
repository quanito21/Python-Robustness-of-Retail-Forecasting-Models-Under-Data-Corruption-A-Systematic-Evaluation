# Robustness of Retail Forecasting Models Under Data Corruption

This project evaluates how various forecasting architectures—ranging from traditional statistical models to deep learning—handle real-world data "messiness." By introducing a Systematic Corruption Framework, I demonstrate that model precision on clean data does not always translate to reliability in production.

## Project Overview
In retail, data is rarely pristine. It is often plagued by missing values, sensor noise, and manual entry errors. This project benchmarks ARIMA, Prophet, Random Forest, XGBoost, and LSTM models to determine which architectures are most resilient to data degradation and introduces a "Noise-Aware" training strategy to mitigate performance loss.

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

| Model | Clean Data (MAPE) | Corrupted Data (MAPE) | Natural Robustness |
| :--- | :---: | :---: | :---: |
| ARIMA | 12.4% | 31.8% | Low |
| Prophet | 10.1% | 28.5% | Moderate |
| XGBoost | 5.2% | 19.4% | Moderate |
| LSTM | 4.1% | 22.3% | Low |
| Random Forest | 6.8% | 11.7% | High |

### The Noise-Aware Breakthrough
While the LSTM was the most precise on clean data, it was brittle. The Random Forest showed the best natural resilience. By applying Noise-Aware training to the Random Forest, I achieved a significant jump in reliability:

| Metric | Original RF | Noise-Aware RF | Improvement |
| :--- | :---: | :---: | :---: |
| Robustness Score | 57.92% | 98.80% | +40.88% |

## Key Takeaways
* Complexity vs. Resilience: Deep learning models (LSTM) provide the highest precision but are the most sensitive to data corruption.
* Ensemble Advantage: Random Forest and XGBoost offer a better balance of accuracy and stability for "messy" real-world applications.
* Training Strategy Matters: You don't always need a more complex model; sometimes you just need a training strategy that simulates the "dirtiness" of the real world.

## Technologies Used
* Modeling: Scikit-learn, XGBoost, TensorFlow (Keras), Prophet, Statsmodels.
* Data Science: Pandas, NumPy, Matplotlib.
* Environment: Jupyter Notebook / Python 3.x.
