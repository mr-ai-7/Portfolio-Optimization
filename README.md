# Portfolio Optimization with PCA

Can a portfolio built from patterns in stock returns outperform equal weighting? This project compares PCA-based portfolios using adjusted closing prices for 30 historical Dow stocks. It selects the portfolio on earlier dates and measures its performance on later dates.

[Open the executed notebook](Eigen%20Portfolio.ipynb) · [View the price data](Dow_adjcloses.csv)

## Dataset and method

The CSV contains 4,804 trading dates from January 3, 2000, through February 6, 2019. The analysis splits daily returns chronologically (80% training, 20% test). It uses the 28 tickers with complete training returns. DWDP and V have incomplete histories. Daily market moves are retained.

The notebook summarizes individual stock returns and plots pairwise correlations. It fits a scaler and PCA on training returns, converts each component into weights that sum to one, and selects the viable candidate with the highest training Sharpe ratio. Ticker labels align the weights with the daily returns. The first ten components explain 71.27% of training variance.

## Historical test results

The selected component was **PC1**. Both portfolios use the same 961 test dates, from 2015-04-15 through 2019-02-06.

| Portfolio | Annualized compounded return | Annualized volatility | Sharpe ratio |
| --- | ---: | ---: | ---: |
| PC1 | 12.17% | 13.43% | 0.92 |
| Equal weight | 12.33% | 13.28% | 0.94 |

The Sharpe ratio uses the arithmetic mean daily return, daily sample volatility, 252 trading days per year, and a zero risk-free rate. The simulation assumes daily rebalancing and excludes trading costs and borrowing fees. Component weights can include shorts. The historical ticker list also limits how well these results represent an investable Dow strategy across the full period.

## Run locally

Extract all files into one folder and open a terminal there.

```bash
python -m pip install -r requirements.txt
python -m notebook "Eigen Portfolio.ipynb"
```

Run the notebook from top to bottom. The included CSV supplies all prices. The saved notebook also displays the results and plots directly on GitHub.
