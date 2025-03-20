# Stock Market Prediction Tool

A machine learning-based tool for analyzing and predicting stock price movements using XGBoost regression models and technical indicators.

## Overview

This tool processes historical stock data for multiple tickers, generates technical indicators, trains XGBoost models, and provides next-day return predictions along with comprehensive evaluation metrics and visualizations.

## Features

- **Automated Multi-Stock Analysis**: Process an entire list of stock tickers automatically
- **Technical Indicator Generation**: Calculate RSI, moving averages, and comprehensive technical indicators
- **Machine Learning Implementation**: XGBoost regression for return prediction
- **Performance Evaluation**: Comprehensive metrics including MSE, RMSE, MAE, R2, and Error/Return Ratio
- **Classification Performance**: Precision, Recall, F1 Score, and AUC-ROC for directional prediction accuracy
- **Visualizations**: Regression plots and confusion matrices 
- **Ranking System**: Stocks ranked by predicted returns
- **Robust Error Handling**: Graceful handling of data issues
- **Progress Tracking**: Resume-capable processing with intermediate results

## Prerequisites

- Google Colab environment
- Google Drive mounted with appropriate directory structure
- CSV file with tickers list (must have a 'Ticker' column)

## Required Libraries

```
tqdm
ta
yfinance
xgboost
scikit-learn==1.2.2
pandas
numpy
matplotlib
seaborn
```

## Setup Instructions

1. Upload the script to Google Colab
2. Create a CSV file named 'Tickers.csv' with a 'Ticker' column containing stock symbols to analyze
3. Place the Tickers.csv file in your Google Drive
4. Update the `base_dir` variable in the script to point to your desired Google Drive directory
5. Run the script

## Directory Structure

The script creates and uses the following directory structure:

```
base_dir/
├── Tickers.csv
├── companies/
│   └── ranked_companies.csv
└── results/
    └── [TICKER]/
        ├── metrics.csv
        ├── regression_plot.png
        └── confusion_matrix.png
```

## Processing Pipeline

1. **Data Collection**: Download historical stock data using Yahoo Finance
2. **Data Preprocessing**:
   - Log-transform prices and volume
   - Calculate log returns
   - Generate stationary features (differenced logs)
   - Create technical indicators using TA library
   - Handle missing values and outliers
3. **Model Training**:
   - Split data into training and test sets (80/20 by default)
   - Train an XGBoost regressor model
4. **Evaluation**:
   - Calculate regression metrics (MSE, RMSE, MAE, R2)
   - Calculate classification metrics (Precision, Recall, F1, AUC-ROC)
   - Generate visualizations
5. **Prediction**:
   - Train a final model on the full dataset
   - Predict the next-day return
6. **Result Storage**:
   - Save metrics, visualizations, and rankings

## Output and Analysis

For each stock, the tool generates:

1. **Regression Metrics**: MSE, RMSE, MAE, R2, Error/Return Ratio
2. **Classification Metrics**: Precision, Recall, F1 Score, AUC-ROC
3. **Visualizations**:
   - Regression plot comparing actual vs. predicted returns
   - Confusion matrix for directional accuracy
4. **Predictions**:
   - Percentage return for the next period
   - Price ratio (>1 for increase, <1 for decrease)

All stocks are ranked in a consolidated CSV file based on predicted returns.

## Customization

You can customize the following parameters:

- `train_size_ratio`: Proportion of data used for training (default: 0.8)
- XGBoost parameters in the model instantiation sections
- Technical indicator windows and feature generation

## Limitations

- Relies on historical data and technical indicators
- Market sentiment and external factors not considered
- Past performance does not guarantee future results
- Models should be periodically retrained with new data

## Notes

- The tool automatically handles symbols with special characters by replacing them with underscores
- Processing can be interrupted and resumed, as it tracks already processed tickers
- Logs are provided for monitoring progress and debugging

## Disclaimer

This tool is for educational and research purposes only. It should not be used as the sole basis for investment decisions. Always consult with a financial advisor before making investment choices.
