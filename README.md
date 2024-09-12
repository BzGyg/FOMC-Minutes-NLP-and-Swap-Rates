# Analyzing FOMC Impact: Leveraging NLP for Sentiment Scores and Swap Rate Predictions

## Overview

This project leverages Natural Language Processing (NLP) to analyze the impact of Federal Open Market Committee (FOMC) statements on swap rates. In our example, we generate sentiment scores using pre-trained FinBERT model and integrate them, along with VIX rates and historical federal swap rates, into a regression model to predict 2-year federal swap rates for the next term.

## Requirements

- [MATLAB](https://www.mathworks.com/products/matlab.html) for the computational environment.
- [FinBERT for MATLAB](https://github.com/matlab-deep-learning/transformer-models) for sentiment analysis.
- Place the data files and FinBERT package folder in your directory.
- Run `Project_Final.mlx`, use `scores.mat` if it is needed.

## Data Sources

- **Swap Rate Data**: Obtained from [Federal Reserve Bank St.Louis](https://fred.stlouisfed.org/categories/32299) and [Bloomberg](https://www.bloomberg.com/professional/products/bloomberg-terminal/).
- **FOMC Data**: Obtain from [FOMC Calendar](https://www.federalreserve.gov/monetarypolicy/fomccalendars.htm) and [FOMC History](https://www.federalreserve.gov/monetarypolicy/fomc_historical_year.htm).
- **VIX Rate Data**: Obain from [Yahoo Finance](https://finance.yahoo.com/quote/%5EVIX/history/).

## File Descriptions

- **`Project_Final.mlx`**: Generates sentiment scores, provides regression analysis and model comparison.
- **`Scores.mat`**: Sentiment scores generated from Mar 2000 to Jul 2024.
- **`DSWP2.csv & WSWP2.csv`**: 2-year daily & weekly swap rates.
- **`swap-libor.xlsx`**: complementary files for 2-year swap rates, daily basis.
- **`DVIX.csv & WVIX.csv`**: daily & weekly CBOE Volatility Index (VIX rates).

## Contact

For questions or suggestions, please contact:

- Email: [Youli Guo](mailto:youliguo0530@gmail.com)
