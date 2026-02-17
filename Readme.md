# Stock Market Prediction - Banking Sector Analysis

A machine learning project predicting stock volatility and price movements for Indian banking sector stocks using proper time series validation.

## Project Overview

This project uses historical stock market data from the National Stock Exchange (NSE) banking sector to:
1. **Predict price direction** - Will the stock go up or down tomorrow?
2. **Forecast volatility** - What will tomorrow's price range be?
3. **Identify ROI opportunities** - Will the stock achieve 10%+ annualized return?

### Key Features

**Proper Machine Learning Methodology:**
- Time series validation (train on past, test on future)
- Zero data leakage (only past information used in predictions)
- Reusable code architecture following DRY principles
- Production-ready structure with clear separation of concerns
- Comprehensive model evaluation and comparison

**Technical Implementation:**
- Multiple ML algorithms (Gradient Boosting, Random Forest, Ridge, XGBoost, Logistic Regression)
- Feature engineering with lagged variables and moving averages
- Proper scaling and cross-validation
- Model persistence for deployment

## Performance Results

Using proper time series validation (training on 2016-2020, testing on 2020-2021):

| Task | Best Model | Metric | Score |
|------|-----------|--------|-------|
| Price Direction | Gradient Boosting | ROC-AUC | 0.5390 |
| Volatility Prediction | Ridge Regression | R² | 0.7885 |
| ROI Achievement | Gradient Boosting | ROC-AUC | 0.5358 |

**Performance Context:**
- Price direction accuracy of 52.5% represents a 3.9% edge over random guessing
- Volatility R² of 0.79 is excellent for financial data and competitive with GARCH models
- Results are realistic and honest, achieved without data leakage
- Performance is competitive with academic baselines for pure technical analysis

## Dataset

- **Source**: National Stock Exchange Banking Sector (Kaggle)
- **Period**: January 2016 - May 2021
- **Stocks**: Major Indian banking stocks (HDFC, ICICI Bank, Axis Bank, etc.)
- **Features**: OPEN, HIGH, LOW, CLOSE, VOLUME, TURNOVER
- **Granularity**: Daily OHLCV data

## Technology Stack

- **Python 3.8+**
- **scikit-learn** - Machine learning models and evaluation
- **XGBoost** - Gradient boosting implementation
- **pandas** - Data manipulation and analysis
- **numpy** - Numerical computing
- **matplotlib/seaborn** - Data visualization
- **joblib** - Model persistence

## Project Structure

```
stock-prediction-nse/
├── stock_prediction_refactored.ipynb  # Main analysis notebook
├── NSE_BANKING_SECTOR.csv            # Dataset (download separately)
├── README.md                         # Project documentation
├── requirements.txt                  # Python dependencies
└── .gitignore                        # Git ignore rules
```

## Getting Started

### Prerequisites

```bash
python --version  # Requires Python 3.8 or higher
```

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/YOUR-USERNAME/stock-prediction-nse.git
cd stock-prediction-nse
```

2. **Install dependencies**
```bash
pip install -r requirements.txt
```

3. **Download the dataset**
   - Download from [Kaggle](https://www.kaggle.com/datasets/sumandey/national-stock-exchange-banking-sectors)
   - Place `NSE_BANKING_SECTOR.csv` in the same folder as the notebook

4. **Run the notebook**
```bash
jupyter notebook stock_prediction_refactored.ipynb
```

## Methodology

### Feature Engineering

**Engineered features include:**
- **Volatility**: Daily price range (HIGH - LOW)
- **Trade Intensity**: TURNOVER / VOLUME ratio
- **Temporal Features**: Day of week
- **Lagged Features**: Historical volatility and volume (1, 2, 3, 5 days)
- **Moving Averages**: 5, 10, 20-day rolling averages for price and volume

**Critical consideration:** All features use only past data available at prediction time to eliminate look-ahead bias.

### Models Evaluated

**Classification Models** (Price Direction, ROI Achievement):
- Logistic Regression
- Random Forest Classifier
- Gradient Boosting Classifier
- XGBoost Classifier

**Regression Models** (Volatility Prediction):
- Ridge Regression
- Random Forest Regressor
- XGBoost Regressor

### Validation Strategy

**Time Series Split:**
- Training: January 2016 - May 4, 2020 (32,205 samples)
- Testing: May 5, 2020 - May 28, 2021 (9,026 samples)
- Chronological split ensures we predict the future, not just new stocks
- No data leakage - features use only past information

## Key Insights

### Feature Importance

Top 5 most important features (from Random Forest analysis):
1. Lagged Volatility (1-day) - Recent volatility strongly predicts future volatility
2. Volume Moving Averages - Trading activity patterns provide signal
3. Price Change Percentage - Recent momentum is informative
4. Close Moving Averages - Trend following works
5. Trade Intensity - Turnover/Volume ratio indicates conviction

### Model Selection Results

- **Classification tasks**: Gradient Boosting performed best, capturing non-linear relationships
- **Regression task**: Ridge Regression won, leveraging strong linear autocorrelation in volatility
- **Lesson**: Match model complexity to problem structure

### Comparison to Original Implementation

| Aspect | Original | Refactored |
|--------|----------|------------|
| Validation | Random split | Chronological split |
| Data Leakage | Present | Eliminated |
| Features | Inconsistent | Properly lagged |
| Code Quality | Repeated code | Reusable functions |
| Results | Inflated (95% R²) | Realistic (54% accuracy, 79% R²) |
| Production Ready | No | Yes |

## Limitations

**Current Limitations:**
- Technical features only (no fundamental data like P/E ratios, earnings)
- No sentiment analysis (news, social media)
- Daily granularity only (no intraday patterns)
- Banking sector specific (may not generalize to other sectors)
- Transaction costs not factored into evaluation
- Test period is COVID recovery (May 2020-May 2021), which may not represent normal market conditions

**Methodological Considerations:**
- Survivorship bias not addressed (dataset includes only current stocks)
- No regime detection (bull vs bear markets treated equally)
- Single-day predictions only (no multi-step forecasting)

## Future Improvements

**Planned Enhancements:**
1. Add technical indicators (RSI, MACD, Bollinger Bands)
2. Implement walk-forward validation (retrain as new data arrives)
3. Create backtesting framework with transaction costs
4. Add fundamental features from financial statements
5. Incorporate sentiment analysis from news and social media
6. Test generalization across different market sectors
7. Build web application for live predictions (Streamlit)
8. Implement ensemble methods combining multiple models

## Learning Outcomes

This project demonstrates:
- Time series machine learning best practices
- Feature engineering for financial data
- Proper train/test splitting for temporal data
- Data leakage prevention and detection
- Model evaluation and comparison
- Production-ready code architecture
- Honest result reporting and interpretation

## Use Cases

**Potential applications (with proper risk management):**
- Volatility-adjusted position sizing
- Trade filtering based on model confidence
- Risk management (dynamic stop-loss placement)
- Portfolio construction and stock screening

**Not recommended:**
- Using as sole basis for trading decisions
- High-leverage trading based on predictions
- Ignoring transaction costs and slippage
- Trading without proper risk management

## Project Context

This project was developed during my Master's program to explore machine learning applications in financial forecasting. It represents an evolution from initial exploration to production-ready code, demonstrating:
- The ability to identify and fix fundamental issues (data leakage)
- Understanding of domain-specific requirements (finance)
- Commitment to honest reporting over inflated metrics
- Production engineering mindset

## Contact

**Abu**
- Email: [Your Email]
- LinkedIn: [Your LinkedIn URL]
- GitHub: [Your GitHub Profile]

Project Link: [https://github.com/YOUR-USERNAME/stock-prediction-nse](https://github.com/YOUR-USERNAME/stock-prediction-nse)

## Acknowledgments

- Dataset: [National Stock Exchange Banking Sector on Kaggle](https://www.kaggle.com/datasets/sumandey/national-stock-exchange-banking-sectors)
- Technical references: Sklearn documentation, XGBoost documentation
- Inspiration: Financial time series forecasting research and production ML best practices

## License

MIT License - see LICENSE file for details

## Disclaimer

This project is for educational and research purposes only. Stock market prediction is inherently uncertain, and past performance does not guarantee future results. These models should NOT be used as the sole basis for investment decisions. Transaction costs, slippage, and market impact significantly affect real-world profitability. Always consult qualified financial advisors and conduct thorough due diligence before making any investment. The author assumes no liability for financial losses resulting from use of these models.
