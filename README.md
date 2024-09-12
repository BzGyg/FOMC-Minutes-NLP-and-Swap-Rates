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

### Daily

Dmdl_1 = 
Linear regression model:
    Future_Swap_Rate ~ Current_Swap_Rate + Latest_VIX_Rate + Second_Latest_VIX_Rate

Estimated Coefficients:
                               Estimate        SE         tStat       pValue  
                              __________    _________    _______    __________

    Current_Swap_Rate            0.98058    0.0025931     378.16             0
    Latest_VIX_Rate           -0.0066958    0.0016401    -4.0825    4.5127e-05
    Second_Latest_VIX_Rate     0.0083686    0.0016365     5.1138    3.2549e-07


Number of observations: 5993, Error degrees of freedom: 5990
Root Mean Squared Error: 0.392

Dmdl_2 = 
Linear regression model:
    Future_Swap_Rate ~ Sentiment_Score + Current_Swap_Rate + Latest_VIX_Rate + Second_Latest_VIX_Rate

Estimated Coefficients:
                               Estimate        SE         tStat       pValue  
                              __________    _________    _______    __________

    Sentiment_Score              0.50131      0.11174     4.4863    7.3835e-06
    Current_Swap_Rate            0.97497    0.0028751     339.12             0
    Latest_VIX_Rate           -0.0071033      0.00164    -4.3313    1.5067e-05
    Second_Latest_VIX_Rate     0.0079314    0.0016368     4.8458    1.2929e-06


Number of observations: 5993, Error degrees of freedom: 5989
Root Mean Squared Error: 0.391

### Weekly

Wmdl_1 = 
Linear regression model:
    Future_Swap_Rate ~ Current_Swap_Rate + Latest_VIX_Rate + Second_Latest_VIX_Rate

Estimated Coefficients:
                               Estimate        SE         tStat       pValue  
                              __________    _________    _______    __________

    Current_Swap_Rate             1.0012     0.001679     596.35             0
    Latest_VIX_Rate           -0.0061696    0.0010584    -5.8291    7.4686e-09
    Second_Latest_VIX_Rate     0.0055681    0.0010579     5.2635    1.7233e-07


Number of observations: 1023, Error degrees of freedom: 1020
Root Mean Squared Error: 0.11

Wmdl_2 = 
Linear regression model:
    Future_Swap_Rate ~ Sentiment_Score + Current_Swap_Rate + Latest_VIX_Rate + Second_Latest_VIX_Rate

Estimated Coefficients:
                               Estimate        SE         tStat       pValue  
                              __________    _________    _______    __________

    Sentiment_Score              0.34291     0.074087     4.6284    4.1596e-06
    Current_Swap_Rate            0.99722    0.0018758     531.62             0
    Latest_VIX_Rate           -0.0064818    0.0010501    -6.1723    9.6988e-10
    Second_Latest_VIX_Rate     0.0053942    0.0010481     5.1465    3.1826e-07


Number of observations: 1023, Error degrees of freedom: 1019
Root Mean Squared Error: 0.109

### Comparison

Adjusted R-squared : 

                    Models                     AdjRSquare
    _______________________________________    __________

    {'Daily Models w.o. Sentiment Scores' }     0.94689  
    {'Daily Models w.t. Sentiment Scores' }     0.94706  
    {'Weekly Models w.o. Sentiment Scores'}     0.99602  
    {'Weekly Models w.t. Sentiment Scores'}      0.9961  

F-test Results :

Daily_f = 20.1266
Daily P-value = 7.3835e-06

Weekly_f = 21.4223
Weekly P-value = 4.1596e-06

## Contact

For any suggestions, please contact:

- Email: [Youli Guo](mailto:youliguo0530@gmail.com); [Rijul Gupta]; [Xidan Liang].
