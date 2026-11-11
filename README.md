# Low-Risk Portfolio Optimisation in R

Risk-return analysis of 10 US stocks and a **minimum-variance portfolio** for a conservative investor with $1.5 million who wants to protect their savings. The project uses real market data, statistical inference and quadratic optimisation.

> Originally part of a team project for ECOM5002 Quantitative Methods for Business at Curtin University (2026). This repository contains **my parts**: data preparation, the stock analysis and the low-risk portfolio.

## Data
- Daily adjusted prices for 10 US stocks (AAPL, AXP, BBY, CRM, DUK, MA, NEU, NFLX, NKE, XOM) from **Yahoo Finance**
- The US Federal Funds Rate from **FRED**, used as the risk-free return
- Converted to **140 monthly returns** (Jan 2015 to Aug 2026), then split into a 120-month estimation sample and a 20-month hold-out sample that was not used to build the portfolio
- Data is downloaded live each time the report is knitted, with quality checks for missing values and date coverage

## What I did
1. **Risk and return analysis:** mean return, volatility, Sharpe ratio, worst month and maximum drawdown for each stock
2. **Statistical inference:** 95% confidence intervals for expected returns, Shapiro-Wilk and Jarque-Bera normality tests, and bootstrap intervals for the fat-tailed stocks
3. **Portfolio optimisation:** a long-only minimum-variance portfolio with a 30% cap per stock, solved with quadratic programming (`quadprog`), and checked with marginal risk contributions

## Key results (Jan 2015 to Dec 2024)
| | Volatility (% per month) |
|---|---|
| **Minimum-variance portfolio (30% cap)** | **3.70** |
| Equal-weight portfolio | 4.89 |
| Lowest-risk single stock (DUK) | 4.90 |
| Highest-risk single stock (NFLX) | 12.14 |

- The optimised portfolio is **about 24% less volatile** than an equal-weight portfolio and less volatile than any single stock.
- Expected return is 0.99% per month, with a Sharpe ratio of 0.229. Its worst month was −9.74%, compared with −49.18% for NFLX.
- **AAPL** had the best risk-adjusted return (Sharpe 0.266), but the confidence intervals overlap heavily, so the differences between stocks are not statistically clear.
- Four stocks (AXP, CRM, NFLX, XOM) have **fat-tailed returns**. Bootstrap intervals confirmed the t-intervals are still reliable for the mean.
- The 30% cap spreads the money across more stocks for only a small cost in risk (3.70% against 3.57% without the cap).

<!-- Add charts here after knitting, e.g. ![Risk and return](images/risk_return.png) -->

## Team result
In the full team project, this low-risk portfolio was combined 50:50 with a growth portfolio. On the 20 unseen months (Jan 2025 to Aug 2026), the combined portfolio gained **24.5%** and was the least volatile of the three portfolios.

## Limitations
- Results are historical and based on only 10 stocks, so they may not repeat.
- Variance treats gains and losses the same, and may understate extreme losses for fat-tailed stocks.
- Transaction costs and taxes are ignored.

## Tech stack
R · R Markdown · quantmod · tidyverse · PerformanceAnalytics · quadprog · ggplot2

## How to run
Open `portfolio_analysis.Rmd` in RStudio, install the packages above, and click **Knit**. The data downloads automatically.
