# SARIMA and ETS Models for Padma Bridge Toll Traffic Prediction

This directory contains the implementation of SARIMA (Seasonal AutoRegressive Integrated Moving Average) and ETS (Error, Trend, Seasonal) models for predicting toll traffic patterns.

## Models Overview

### SARIMA Model
SARIMA is a statistical model that combines:
- Autoregression (AR): Uses past values to predict future ones
- Integration (I): Differencing to make data stationary
- Moving Average (MA): Uses past error terms for prediction
- Seasonal Component (S): Captures recurring patterns

The model parameters (p,d,q)(P,D,Q)s are automatically determined using auto_arima, which:
- Tests different combinations of parameters
- Evaluates multiple seasonal periods (7, 14, 30 days)
- Selects the best model based on AIC criterion

### ETS Model
ETS modeling provides an alternative approach using exponential smoothing:
- Error: How uncertainty is modeled
- Trend: Direction of data movement
- Seasonal: Recurring patterns
- Multiple configurations tested (additive/multiplicative)

## Data Preparation

1. Data Loading and Cleaning:
    - Load daily toll traffic data
    - Convert date formats and sort chronologically
    - Aggregate multiple daily entries
    - Handle missing values through forward/backward fill

2. Time Series Analysis:
    - STL Decomposition to separate trend, seasonality, and residuals
    - Analysis of seasonal patterns at different frequencies
    - Evaluation of trend and seasonality strength

## Model Implementation

1. **Data Split**:
    - **Training set:** All data except last 60 days
    - **Test set:** Last 60 days for validation

2. **Model Training:**
    - Auto ARIMA for optimal SARIMA parameters
    - Multiple seasonality testing (7, 14, 30 days)
    - ETS model with various configurations
    - Confidence intervals for forecasts

3. **Forecasting:**
    - Short-term (60 days) for model validation
    - Long-term (365 days) future predictions
    - Separate models for different traffic metrics

## Results

The models are trained on multiple target variables:
- Traffic_Mawa
- Traffic_Jajira
- Cash_Mawa
- Cash_Jajira
- Total_Traffic

Performance metrics (MAE, RMSE, R²) are calculated separately for each target variable and model type. Both SARIMA and ETS models show effective capture of:
- Daily and weekly patterns
- Holiday effects
- Long-term trends

## Model Performance Results

### SARIMA Model Performance
| Target Variable | MAE | RMSE | R² | Model Configuration |
|----------------|-----|------|-----|-------------------|
| Traffic_Mawa | 741.31 | 940.20 | -0.2064 | SARIMA(2,1,1)(0,0,0,7) |
| Traffic_Jajira | 1,237.50 | 1,882.97 | -0.0569 | SARIMA(2,1,1)(0,0,0,30) |
| Cash_Mawa | 419,195.22 | 794,080.00 | -0.0009 | SARIMA(1,1,3)(0,0,0,7) |
| Cash_Jajira | 676,110.36 | 1,241,030.00 | **0.0015** | SARIMA(0,1,4) |
| Total_Traffic | 2,126.95 | 2,859.26 | -0.1737 | SARIMA(2,1,2)(1,0,0,7) |

### ETS Model Performance
| Target Variable | MAE | RMSE | R² | Configuration |
|----------------|-----|------|-----|---------------|
| Traffic_Mawa | 636.38 | 1,069.94 | -0.5623 | MAM |
| Traffic_Jajira | 1,426.78 | 2,031.60 | -0.2304 | MAM |
| Cash_Mawa | 1,451,049.02 | 2,037,648.36 | -5.5903 | MAM |
| Cash_Jajira | 1,761,894.80 | 2,294,176.26 | -2.4121 | MAM |
| Total_Traffic | 1,907.86 | 2,941.93 | -0.2425 | MAM |

Note: 
- MAM = Multiplicative Error, Additive Trend, Multiplicative Seasonal

Key Findings:
- Both SARIMA and ETS models show challenges in capturing the complex patterns in the data
- SARIMA models mostly use weekly (7-day) seasonality, with one case of monthly (30-day) seasonality
- Best performance achieved by SARIMA for Cash_Jajira with a slightly positive R² of 0.0015
- Most models show negative R² values, indicating difficulty in beating the mean prediction
- All ETS models converged to MAM configuration, suggesting multiplicative seasonality in the data