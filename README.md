## Padma Bridge Toll Prediction Notebooks

This repository contains time series forecasting models for predicting traffic volume and cash collection at Padma Bridge toll stations. Multiple approaches are implemented and compared, including ARIMA, SARIMA, LSTM, Random Forest, LightGBM, and XGBoost.

---

### Project Structure
- **Dataset/**: Contains the raw data (`Padma_Bridge.csv`).
- **ARIMA/**, **SARIMA/**, **LSTM/**, **Random Forest/**, **LightGBM/**, **XGBoost/**: Each folder contains a notebook and README for the respective model.

---

### Models Overview
| Model         | Description                                      |
|-------------- |--------------------------------------------------|
| ARIMA         | Classical statistical model for univariate time series forecasting. |
| SARIMA        | Extension of ARIMA with seasonality.             |
| LSTM          | Deep learning model for sequential data.          |
| Random Forest | Ensemble tree-based regression.                   |
| LightGBM      | Gradient boosting framework for fast, accurate predictions. |
| XGBoost       | Extreme Gradient Boosting, optimized for speed and performance. |

---

### Comparative Results

R² (%) values indicate the proportion of variance explained by each model for each target variable (higher is better).

| Model         | Traffic_Mawa | Traffic_Jajira | Cash_Mawa | Cash_Jajira | Total_Cash | Total_Traffic |
|-------------- |------------- |--------------- |-----------|-------------|------------|---------------|
| SARIMA        | -0.21        | -0.06          | -0.0009   | 0.0015      |            | -0.17         |
| LSTM          | -0.035       |                |           |             |            |               |
| Random Forest | 0.559        | 0.428          | 0.584     | 0.517       | 0.620      | 0.511         |
| LightGBM      | **0.645**    | **0.501**      | **0.615** | 0.322       | **0.687**  | **0.671**     |

---

### Key Findings
- **LightGBM** achieved the highest R² values for most target variables.

- **XGBoost** performed best for Cash_Jajira, but was slightly behind LightGBM for other targets.
- **Random Forest** provided solid results, especially for Total_Cash, but was outperformed by boosting methods.
- **SARIMA** and **LSTM** models had negative or near-zero R² values, showing poor fit for this dataset and feature set.
- Tree-based and boosting models (LightGBM, XGBoost, Random Forest) consistently outperformed classical time series and deep learning approaches in this application.
- Feature engineering and hyperparameter tuning were critical for achieving high accuracy in machine learning models.