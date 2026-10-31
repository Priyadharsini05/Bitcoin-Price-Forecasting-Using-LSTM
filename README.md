# Bitcoin Price Prediction Using LSTM

## Overview

This project implements a **multivariate time-series forecasting model using Long Short-Term Memory (LSTM) neural networks** to predict future Bitcoin market prices.

The model learns temporal patterns from historical cryptocurrency market data and predicts multiple market features using a sliding-window approach. The project also compares predicted and actual bid and ask prices and evaluates potential trading opportunities by analyzing cumulative price differences, including transaction fees.

## Key Features

- **Multivariate Time-Series Forecasting:** Uses multiple market features to learn temporal dependencies.
- **LSTM-Based Deep Learning:** Implements a stacked LSTM network to capture sequential patterns in historical market data.
- **Sliding-Window Prediction:** Uses the previous 50 time steps to predict subsequent market values.
- **Future Price Forecasting:** Generates predictions for the next 20 time steps.
- **Model Evaluation:** Evaluates the trained model using mean squared error (MSE) loss.
- **Actual vs. Predicted Visualization:** Compares predicted bid and ask prices against actual market values.
- **Trading Opportunity Analysis:** Examines predicted price movements to identify potentially favorable trading opportunities.
- **Transaction Fee Analysis:** Incorporates a 0.1% taker fee into the trading profitability analysis.

## Technologies Used

- **Programming Language:** Python
- **Data Processing:** Pandas, NumPy
- **Data Visualization:** Matplotlib
- **Machine Learning:** Scikit-learn
- **Deep Learning:** TensorFlow/Keras
- **Model Architecture:** Long Short-Term Memory (LSTM)
- **Data Preprocessing:** MinMaxScaler

## Model Architecture

The project uses a sequential deep learning model consisting of four LSTM layers and dropout regularization.

| Component | Configuration |
|---|---|
| Input sequence length | 50 time steps |
| First LSTM layer | 50 units |
| Second LSTM layer | 50 units |
| Third LSTM layer | 50 units |
| Fourth LSTM layer | 50 units |
| Dropout rate | 20% after each LSTM layer |
| Output layer | Dense layer with 9 units |
| Loss function | Mean Squared Error (MSE) |
| Optimizer | Adam |
| Batch size | 32 |
| Training epochs | 15 |

The model processes historical sequences containing nine input features and predicts the corresponding values for the next time step.

## Methodology

### 1. Data Loading and Preprocessing

The historical cryptocurrency market dataset is loaded using Pandas.

Several columns that are not used in the model are removed, including exchange identifiers, volume averages, trade counts, daily highs and lows, and opening prices.

The remaining numerical features are normalized to the range of 0 to 1 using `MinMaxScaler`.

### 2. Training and Testing Split

The dataset is divided chronologically into training and testing subsets.

- **Training data:** Approximately 80% of the dataset.
- **Testing data:** The remaining observations.

This approach preserves the original order of the time-series observations.

### 3. Sequence Generation

A sliding-window approach generates the input sequences required for LSTM training.

For each training example:
- The previous 50 time steps form the input sequence.
- The market features at the next time step form the prediction target.

The resulting sequences are converted into NumPy arrays before being passed to the neural network.

### 4. LSTM Model Training

The model is trained using four stacked LSTM layers, dropout regularization, the Adam optimizer, and mean squared error loss.

The trained model is saved as an HDF5 file for later use.

### 5. Model Evaluation

The model is evaluated on the test sequences using the configured loss function.

Predictions are transformed back to their original feature scales to facilitate comparison with the actual market values.

### 6. Future Price Prediction

The trained model predicts the next 20 time steps using a moving-window forecasting function.

After each prediction, the oldest time step is removed from the input window, and the predicted values are appended to generate the next input sequence.

This allows the model to produce successive predictions without requiring actual market observations for every future time step.

### 7. Trading Opportunity Analysis

The project analyzes predicted bid and ask prices to identify potential opportunities based on projected price differences.

It also calculates cumulative price differences for selected opportunities and compares predicted values with observed market prices.

A transaction-fee-aware analysis incorporates a taker fee of 0.1% on buying and selling prices to examine how trading costs affect the projected opportunities.

## Project Workflow

```text
Historical Cryptocurrency Market Data
                 |
                 v
       Data Cleaning and Selection
                 |
                 v
        Feature Normalization
                 |
                 v
       Training / Testing Split
                 |
                 v
        Sliding-Window Sequences
                 |
                 v
          Stacked LSTM Model
                 |
                 v
           Model Evaluation
                 |
                 v
      Future Market Price Forecasting
                 |
                 v
      Bid/Ask Price Comparison
                 |
                 v
       Trading Opportunity Analysis
                 |
                 v
       Transaction Fee Evaluation
```

## Visualizations

The notebook generates visualizations for:

- Actual versus predicted ask prices.
- Actual versus predicted bid prices.
- Forecasted bid and ask prices over future time steps.
- Cumulative price differences from selected trading opportunities.
- Comparison of predicted and observed cumulative price differences after accounting for transaction fees.

These visualizations help examine the model's forecasting behavior and the potential implications of its predictions.

## Installation

### Prerequisites

- Python 3.9 or later
- Jupyter Notebook or Google Colab

### Install Dependencies

```bash
pip install pandas numpy matplotlib scikit-learn tensorflow
```

## How to Run

1. Clone or download this repository.
2. Open the Jupyter Notebook in Jupyter or Google Colab.
3. Place the historical market dataset in an accessible location.
4. Update the dataset path in the notebook to match your environment.
5. Run the notebook cells sequentially.
6. Review the model evaluation output, prediction plots, and trading analysis.

**Note:** The notebook expects a CSV dataset named `data_mv_set.csv`. The original notebook references a local Windows file path, which must be updated before running the project on another machine.

## Model Output

The notebook produces:

- A trained LSTM model saved in HDF5 format.
- Predictions for historical test sequences.
- Forecasts for 20 future time steps.
- Actual-versus-predicted bid and ask price plots.
- Cumulative trading opportunity comparisons, including transaction-fee analysis.

## Limitations

- Cryptocurrency prices are volatile and influenced by external factors that historical market data may not capture.
- Multi-step forecasts can accumulate prediction errors because previous predictions are reused as subsequent inputs.
- The model's loss value alone does not establish the profitability of a trading strategy.
- Transaction-fee calculations do not establish real-world profitability and may not account for slippage, liquidity constraints, latency, or other trading costs.
- The notebook's results depend on the quality, feature definitions, and time coverage of the supplied dataset.
- The model should be evaluated using appropriate forecasting metrics and realistic backtesting before any practical trading application.

**Important:** This project is intended for educational and research purposes. Its predictions should not be treated as financial advice or as a guarantee of future cryptocurrency prices.

## Future Improvements

- Evaluate forecasts using MAE, RMSE, and other appropriate regression metrics.
- Improve time-series validation and prevent data leakage during preprocessing.
- Compare LSTM performance against GRU, Transformer, and statistical forecasting models.
- Experiment with different sequence lengths and model hyperparameters.
- Incorporate additional market indicators and historical trading features.
- Develop a more realistic backtesting framework with transaction costs and risk-adjusted performance metrics.
- Build an interactive dashboard for exploring historical prices and model forecasts.

## Conclusion

This project demonstrates the application of **deep learning and multivariate time-series forecasting to cryptocurrency market analysis**. By combining a stacked LSTM architecture, sliding-window predictions, bid/ask price visualization, and transaction-fee-aware trading analysis, it provides a foundation for further experimentation with cryptocurrency forecasting models.

---

**Topics:** `Python` `Deep Learning` `LSTM` `Bitcoin` `Cryptocurrency` `Time Series Forecasting` `Price Prediction` `TensorFlow` `Keras` `Machine Learning` `Financial Data Analysis`
