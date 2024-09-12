# Analyzing FOMC Impact: Leveraging NLP for Sentiment Scores and Swap Rate Predictions

## Overview

This project leverages Natural Language Processing (NLP) to analyze the impact of Federal Open Market Committee (FOMC) statements on swap rates. We utilize FinBERT for sentiment analysis on FOMC documents and MATLAB for forecasting swap rates.

## Requirements

To run this project, you will need:
- [MATLAB](https://www.mathworks.com/products/matlab.html) for the computational environment.
- [FinBERT for MATLAB](https://github.com/matlab-deep-learning/transformer-models) for sentiment analysis.

## Data Sources

- **Two-Year Swap Rate Data**: Available in `DSWP2.csv`, `WSWP2.csv`, and `swap-libor.xlsx`
- **FOMC Data**: Obtain from the [FOMC Calendar](https://www.federalreserve.gov/monetarypolicy/fomccalendars.htm)

## File Descriptions

- **`Scoring.mlx`**: Contains details on FOMC fetching and sentiment scoring.
- **`Project_Final.mlx`**: Provides regression analysis and model comparison.

## Installation and Setup

1. Ensure MATLAB R2023b or newer is installed with the required toolboxes and apps.
2. Download the project files from the repository.
3. Place the data files (`DSWP2.csv`, `WSWP2.csv`, `swap-libor.xlsx`) and FOMC Calendar files in the project directory.

## Usage

1. Open MATLAB and navigate to the project directory.
2. Run the `Scoring.mlx` script to fetch FOMC data and perform sentiment analysis.
3. Use the `Project_Final.mlx` script for regression analysis and model comparison.

## Contributing

If you would like to contribute to this project, please:

1. Fork the repository.
2. Create a new branch (`git checkout -b feature-branch`).
3. Make your changes.
4. Commit your changes (`git commit -am 'Add new feature'`).
5. Push to the branch (`git push origin feature-branch`).
6. Create a Pull Request.

## Contact

For questions or suggestions, please contact:

- Email: [Youli Guo](mailto:youliguo0530@gmail.com)
