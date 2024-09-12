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
- **`Scores.mat`**: Sentiment scores with corresponding dates generated from Mar 2000 to Jul 2024.
- **`DSWP2.csv & WSWP2.csv`**: 2-year daily & weekly swap rates.
- **`swap-libor.xlsx`**: Complementary files for 2-year swap rates, daily basis.
- **`DVIX.csv & WVIX.csv`**: Daily & weekly CBOE Volatility Index (VIX rates).

## Our Results

### Daily Models

#### Dmdl_1
**Linear Regression Model**  
*Dependent Variable:* Future_Swap_Rate  
*Independent Variables:*  
- Current_Swap_Rate  
- Latest_VIX_Rate  
- Second_Latest_VIX_Rate

| Variable                 | Estimate | SE       | t-Stat  | p-Value      |
|--------------------------|----------|----------|---------|--------------|
| **Current_Swap_Rate**     | 0.98058  | 0.0025931| 378.16  | 0            |
| **Latest_VIX_Rate**       | -0.0067  | 0.0016401| -4.08   | 4.51e-05     |
| **Second_Latest_VIX_Rate**| 0.00837  | 0.0016365| 5.11    | 3.25e-07     |

- **Number of Observations:** 5993  
- **Degrees of Freedom:** 5990  
- **Root Mean Squared Error:** 0.392

#### Dmdl_2
**Linear Regression Model**  
*Dependent Variable:* Future_Swap_Rate  
*Independent Variables:*  
- Sentiment_Score  
- Current_Swap_Rate  
- Latest_VIX_Rate  
- Second_Latest_VIX_Rate

| Variable                 | Estimate | SE       | t-Stat  | p-Value      |
|--------------------------|----------|----------|---------|--------------|
| **Sentiment_Score**       | 0.50131  | 0.11174  | 4.49    | 7.38e-06     |
| **Current_Swap_Rate**     | 0.97497  | 0.0028751| 339.12  | 0            |
| **Latest_VIX_Rate**       | -0.0071  | 0.00164  | -4.33   | 1.51e-05     |
| **Second_Latest_VIX_Rate**| 0.00793  | 0.0016368| 4.85    | 1.29e-06     |

- **Number of Observations:** 5993  
- **Degrees of Freedom:** 5989  
- **Root Mean Squared Error:** 0.391

### Weekly Models

#### Wmdl_1
**Linear Regression Model**  
*Dependent Variable:* Future_Swap_Rate  
*Independent Variables:*  
- Current_Swap_Rate  
- Latest_VIX_Rate  
- Second_Latest_VIX_Rate

| Variable                 | Estimate | SE       | t-Stat  | p-Value      |
|--------------------------|----------|----------|---------|--------------|
| **Current_Swap_Rate**     | 1.0012   | 0.001679 | 596.35  | 0            |
| **Latest_VIX_Rate**       | -0.00617 | 0.0010584| -5.83   | 7.47e-09     |
| **Second_Latest_VIX_Rate**| 0.00557  | 0.0010579| 5.26    | 1.72e-07     |

- **Number of Observations:** 1023  
- **Degrees of Freedom:** 1020  
- **Root Mean Squared Error:** 0.11

#### Wmdl_2
**Linear Regression Model**  
*Dependent Variable:* Future_Swap_Rate  
*Independent Variables:*  
- Sentiment_Score  
- Current_Swap_Rate  
- Latest_VIX_Rate  
- Second_Latest_VIX_Rate

| Variable                 | Estimate | SE       | t-Stat  | p-Value      |
|--------------------------|----------|----------|---------|--------------|
| **Sentiment_Score**       | 0.34291  | 0.074087 | 4.63    | 4.16e-06     |
| **Current_Swap_Rate**     | 0.99722  | 0.0018758| 531.62  | 0            |
| **Latest_VIX_Rate**       | -0.00648 | 0.0010501| -6.17   | 9.70e-10     |
| **Second_Latest_VIX_Rate**| 0.00539  | 0.0010481| 5.15    | 3.18e-07     |

- **Number of Observations:** 1023  
- **Degrees of Freedom:** 1019  
- **Root Mean Squared Error:** 0.109

### Model Comparison

| Models                                | Adjusted R-Squared |
|---------------------------------------|--------------------|
| **Daily Models w/o Sentiment Scores** | 0.94689            |
| **Daily Models w/ Sentiment Scores**  | 0.94706            |
| **Weekly Models w/o Sentiment Scores**| 0.99602            |
| **Weekly Models w/ Sentiment Scores** | 0.9961             |

### F-Test Results

- **Daily Models:**  
  F-Statistic = 20.1266  
  P-Value = 7.38e-06  

- **Weekly Models:**  
  F-Statistic = 21.4223  
  P-Value = 4.16e-06

## Contact

For any suggestions, please contact:

- Email: [Youli Guo](mailto:youliguo0530@gmail.com); [Rijul Gupta]; [Xidan Liang].
