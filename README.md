# Analyzing FOMC Impact: Leveraging NLP for Sentiment Scores and Swap Rate Predictions

## Overview

This project leverages Natural Language Processing (NLP) to analyze the impact of Federal Open Market Committee (FOMC) statements on swap rates. In our example, we generate sentiment scores using pre-trained FinBERT model and integrate them, along with VIX rates and historical federal swap rates, into a regression model to predict 2-year federal swap rates for the next term.

- **`Project_Final.ipynb`** / **`Project_Final.pdf`**: Printed version of **`Project_Final.mlx`**, serving as the project Report.
- **`Project_Final.mlx`**: Generates sentiment scores, provides regression analysis and model comparison.

## Requirements

- [MATLAB](https://www.mathworks.com/products/matlab.html) for the computational environment.
- [FinBERT for MATLAB](https://github.com/matlab-deep-learning/transformer-models) for sentiment analysis.
- Place the data files and FinBERT package folder in your directory.
- Run `Project_Final.mlx`, use `scores.mat` if it is needed.

## Data Sources

- **Swap Rate Data**: Obtained from [Federal Reserve Bank St.Louis](https://fred.stlouisfed.org/categories/32299) and [Bloomberg](https://www.bloomberg.com/professional/products/bloomberg-terminal/).
- **FOMC Data**: Obtain from [FOMC Calendar](https://www.federalreserve.gov/monetarypolicy/fomccalendars.htm) and [FOMC History](https://www.federalreserve.gov/monetarypolicy/fomc_historical_year.htm).
- **CBOE Volatility Index (VIX rates)**: Obain from [Yahoo Finance](https://finance.yahoo.com/quote/%5EVIX/history/).

## Data Files

- **`Scores.mat`**: Sentiment scores with corresponding dates generated from Mar 2000 to Jul 2024.
- **`DSWP2.csv & WSWP2.csv`**: 2-year daily & weekly swap rates.
- **`swap-libor.xlsx`**: Complementary files for 2-year swap rates, daily basis.
- **`DVIX.csv & WVIX.csv`**: Daily & weekly VIX.

## Methodology

### 1. Data Collection & Preprocessing

**FOMC Minutes Extraction:**
- Web scraping from Federal Reserve websites covering March 2000 to July 2024
- HTML parsing using MATLAB's `htmlTree` and `extractHTMLText` functions
- Text cleaning using signal phrases to isolate economic/financial discussions:
  - **Start signals:** "The information reviewed/provided/received/available...", "Staff Review of the Economic Situation"
  - **End signals:** "At the conclusion of...", "Committee Policy Action", "discussion of monetary policy"
- Filtering paragraphs with length > 100 characters to remove noise

**Swap Rate Data Merging:**
- Combining two data sources (Federal Reserve St. Louis + Bloomberg) with different coverage periods
- Missing value imputation using k-nearest neighbors (`fillmissing` with KNN, k=5)

### 2. Sentiment Analysis

**Model:** FinBERT (Financial Domain BERT)
- Pre-trained transformer model specialized for financial text sentiment classification
- Categories: Positive, Neutral, Negative
- Input: Cleaned and rejoined FOMC minutes text
- Output: Aggregated sentiment scores per document (sum of sentence-level scores)

### 3. Feature Engineering

| Feature | Description | Source |
|---------|-------------|--------|
| `Future_Swap_Rate` | Target variable (next period 2Y swap rate) | Fed St. Louis / Bloomberg |
| `Current_Swap_Rate` | Latest available swap rate before prediction date | Fed St. Louis / Bloomberg |
| `Sentiment_Score` | FinBERT-derived score from FOMC minutes | Computed via FinBERT |
| `Latest_VIX_Rate` | Most recent VIX index value | Yahoo Finance |
| `Second_Latest_VIX_Rate` | Previous period VIX index value | Yahoo Finance |

**Temporal Alignment:**
- Forward-filling applied to match sentiment scores with higher-frequency rate data
- Both daily and weekly frequencies analyzed separately

### 4. Regression Analysis

**Model Specification (no intercept):**

**Model 1 (Baseline):**

```math
\text{Future\_Swap\_Rate} = \beta_1 \cdot \text{Current\_Swap\_Rate} + \beta_2 \cdot \text{VIX}_t + \beta_3 \cdot \text{VIX}_{t-1} + \epsilon
```

**Model 2 (With Sentiment):**

```math
\text{Future\_Swap\_Rate} = \beta_1 \cdot \text{Current\_Swap\_Rate} + \beta_2 \cdot \text{VIX}_t + \beta_3 \cdot \text{VIX}_{t-1} + \beta_4 \cdot \text{Sentiment} + \epsilon
```

**Model Comparison:**
- Adjusted R² comparison between nested models
- F-test for statistical significance of sentiment score contribution:

```math
F = \frac{(SSE_1 - SSE_2) / (df_1 - df_2)}{SSE_2 / df_2}
```

## Results

### Daily Models

#### Dmdl_1 (Baseline)

| Variable                 | Estimate | SE       | t-Stat  | p-Value      |
|--------------------------|----------|----------|---------|--------------|
| **Current_Swap_Rate**     | 0.98058  | 0.0025931| 378.16  | 0            |
| **Latest_VIX_Rate**       | -0.0067  | 0.0016401| -4.08   | 4.51e-05     |
| **Second_Latest_VIX_Rate**| 0.00837  | 0.0016365| 5.11    | 3.25e-07     |

- **Observations:** 5993 | **RMSE:** 0.392

#### Dmdl_2 (With Sentiment)

| Variable                 | Estimate | SE       | t-Stat  | p-Value      |
|--------------------------|----------|----------|---------|--------------|
| **Sentiment_Score**       | 0.50131  | 0.11174  | 4.49    | 7.38e-06     |
| **Current_Swap_Rate**     | 0.97497  | 0.0028751| 339.12  | 0            |
| **Latest_VIX_Rate**       | -0.0071  | 0.00164  | -4.33   | 1.51e-05     |
| **Second_Latest_VIX_Rate**| 0.00793  | 0.0016368| 4.85    | 1.29e-06     |

- **Observations:** 5993 | **RMSE:** 0.391

### Weekly Models

#### Wmdl_1 (Baseline)

| Variable                 | Estimate | SE       | t-Stat  | p-Value      |
|--------------------------|----------|----------|---------|--------------|
| **Current_Swap_Rate**     | 1.0012   | 0.001679 | 596.35  | 0            |
| **Latest_VIX_Rate**       | -0.00617 | 0.0010584| -5.83   | 7.47e-09     |
| **Second_Latest_VIX_Rate**| 0.00557  | 0.0010579| 5.26    | 1.72e-07     |

- **Observations:** 1023 | **RMSE:** 0.11

#### Wmdl_2 (With Sentiment)

| Variable                 | Estimate | SE       | t-Stat  | p-Value      |
|--------------------------|----------|----------|---------|--------------|
| **Sentiment_Score**       | 0.34291  | 0.074087 | 4.63    | 4.16e-06     |
| **Current_Swap_Rate**     | 0.99722  | 0.0018758| 531.62  | 0            |
| **Latest_VIX_Rate**       | -0.00648 | 0.0010501| -6.17   | 9.70e-10     |
| **Second_Latest_VIX_Rate**| 0.00539  | 0.0010481| 5.15    | 3.18e-07     |

- **Observations:** 1023 | **RMSE:** 0.109

### Model Comparison

| Models                                | Adjusted R² |
|---------------------------------------|-------------|
| Daily Models w/o Sentiment Scores     | 0.94689     |
| **Daily Models w/ Sentiment Scores**  | **0.94706** |
| Weekly Models w/o Sentiment Scores    | 0.95602     |
| **Weekly Models w/ Sentiment Scores** | **0.95610** |

### F-Test Results

| Comparison | F-Statistic | P-Value | Conclusion |
|------------|-------------|---------|------------|
| Daily Models | 20.1266 | 7.38e-06 | Significant |
| Weekly Models | 21.4223 | 4.16e-06 | Significant |

## Conclusion

The results demonstrate that sentiment scores derived from FOMC minutes using FinBERT significantly improve the predictive power of swap rate models. Both daily and weekly models show:

1. **Higher Adjusted R²** when sentiment scores are included
2. **Statistically significant F-test results** (p < 0.001), confirming that the sentiment variable adds meaningful explanatory power
3. **Positive sentiment coefficients**, indicating that more positive FOMC sentiment is associated with higher future swap rates

These findings suggest that NLP-based analysis of central bank communications can provide valuable signals for financial market predictions.
