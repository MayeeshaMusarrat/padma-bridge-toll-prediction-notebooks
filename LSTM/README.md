## LSTM Model for Padma Bridge Toll Prediction

### What is LSTM?
LSTM (Long Short-Term Memory) is a type of recurrent neural network (RNN) designed to learn long-term dependencies in sequential data. LSTMs are especially effective for time series forecasting because they can remember patterns over long periods and handle complex temporal relationships.

---

### Data Processing Steps
1. **Data Loading:**
	- The dataset (`Padma_Bridge - Traffic.csv`) is loaded and parsed with pandas. Dates are converted to datetime format and sorted chronologically.
2. **Feature Engineering:**
	- New features are created, including year, month, day, weekend/holiday flags, cyclical encodings (sin/cos), lag features, and rolling statistics (mean, std, min, max, ewm).
3. **Handling Missing Values:**
	- NaN values are dropped after feature creation to ensure clean input for the model.
4. **Train-Test Split:**
	- TimeSeriesSplit is used to split the data into training and testing sets, preserving temporal order.
5. **Sequence Creation:**
	- Data is transformed into sequences suitable for LSTM input, with a specified sequence length.
6. **Scaling:**
	- Target variables are scaled using MinMaxScaler for stable neural network training.

---

### Model Building & Training
1. **LSTM Architecture:**
	- The model consists of an LSTM layer, a dropout layer for regularization, and a dense output layer for multi-target prediction.
2. **Hyperparameter Tuning:**
	- Optuna is used for automated hyperparameter optimization (units, dropout, learning rate, batch size).
3. **Training:**
	- Early stopping and validation split are used to prevent overfitting. The best model is selected based on validation loss.

---

### Results & Evaluation
After training, the model's performance is evaluated using several metrics:

| Metric | Value |
|--------|-------|
| MAE    | 1011869.10|
| MSE    | 5996118722285.44 |
| RMSE   | 2448697.35 |
| R²     | -0.035  |
| MAPE   | 12.81% |