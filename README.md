# Stock Market Prediction — Indian Banking Sector

## Overview

A machine learning project predicting next-day price direction, volatility, and ROI-achievement for Indian banking sector stocks (NSE), using proper time-series validation rather than a random train/test split.

## Business / User Problem

Financial time series are notoriously hard to predict, and naive backtests that shuffle time-ordered data produce inflated, misleading results. This project takes an honest approach: it trains only on the past and tests only on the future, and reports realistic (modest) performance rather than an inflated one — useful as a demonstration of correct methodology as much as a trading signal.

## Key Features

- Time-series validation only — trains on 2016–2020, tests on 2020–2021, never shuffled
- Zero data leakage — only past information is used at prediction time
- Three related prediction tasks: price direction, volatility, and 10%+ annualized ROI achievement
- Systematic comparison across 5 algorithms
- Lagged and moving-average feature engineering

## Tech Stack

- Python 3.8+
- scikit-learn, XGBoost
- pandas, NumPy
- matplotlib, seaborn
- joblib (model persistence)

## Dataset / Inputs

- **Source:** National Stock Exchange (NSE) banking sector data (Kaggle)
- **Period:** January 2016 – May 2021
- **Stocks:** major Indian banking stocks (HDFC, ICICI Bank, Axis Bank, etc.)
- **Features:** daily OHLCV (open, high, low, close, volume, turnover), lagged variables, moving averages
- **Split:** train 2016–2020, test 2020–2021 (temporal, not random)

## Methodology / Architecture

```
Raw OHLCV Data
↓
Feature Engineering (lagged variables, moving averages)
↓
Time-Series Split (train on 2016-2020, test on 2020-2021)
↓
Scaling (fit on train only)
↓
Model Comparison (5 algorithms per task, cross-validated)
↓
Three Prediction Tasks: price direction / volatility / ROI achievement
```

## Results

Using proper time-series validation (train 2016–2020, test 2020–2021):

| Task | Best Model | Metric | Score |
|---|---|---|---|
| Price direction | Gradient Boosting | ROC-AUC | 0.5390 |
| Volatility | Ridge Regression | R² | 0.7885 |
| ROI achievement | Gradient Boosting | ROC-AUC | 0.5358 |

Price-direction prediction is only slightly better than a coin flip (a ~4% edge over random), which is expected and honest for pure technical-analysis features on daily stock direction — this is a known-hard problem in finance, and near-random performance here reflects reality rather than a modeling flaw. Volatility prediction, by contrast, is strong (R² 0.79), competitive with GARCH-style models.

## Screenshots / Demo

_Not yet added. Suggested capture: predicted vs. actual volatility plot._

## Running Locally

```bash
git clone https://github.com/Abu-249607/stock-prediction-nse.git
cd stock-prediction-nse
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
```

Download the NSE banking sector dataset from Kaggle and place it in the project root, then:

```bash
jupyter notebook stock_prediction_refactored.ipynb
```

## Repository Structure

```
stock-prediction-nse/
├── stock_prediction_refactored.ipynb   # Main analysis notebook
├── requirements.txt                     # Python dependencies
└── README.md
```

## Future Improvements

- Add macroeconomic and sentiment features — pure technical indicators have a low ceiling for direction prediction
- Extend to intraday data for shorter-horizon predictions
- Try a walk-forward (rolling-window) validation scheme instead of one fixed split
- Add position-sizing/backtesting logic to translate predictions into a simulated trading strategy
- Compare against a GARCH baseline directly for the volatility task
