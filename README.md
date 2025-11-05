# Regime-Switching Trend Strategy with Volatility Targeting

This project studies how different market volatility regimes affect the performance of trend-following strategies, and how volatility targeting can be used to stabilize risk across those regimes.

---

## Overview

The objective is to design and evaluate a strategy that:

1. Detects market regimes (low-volatility vs. high-volatility periods)
2. Generates a trend-following signal (time-series momentum or moving-average crossover)
3. Applies volatility targeting to maintain a consistent risk profile
4. Backtests and evaluates the combined effect on performance

The focus is on understanding how regime awareness and risk scaling improve Sharpe ratios and drawdown control.

---

## Methodology

1. **Data**
   - Daily prices for liquid assets (e.g. SPY, QQQ, BTC-USD)
   - Returns computed as percentage change of adjusted close

2. **Regime Detection**
   - Option A: 2-state Gaussian Hidden Markov Model (low-vol / high-vol)
   - Option B: Simple volatility-quantile split using rolling 20-day standard deviation

3. **Trend Signal**
   - **Time-Series Momentum (TSMOM):** sign of cumulative return over a lookback window  
   - **Moving Average Crossover (MAC):** +1 if short MA > long MA, else -1

4. **Volatility Targeting**
   - Target annualized volatility (e.g. 10%)
   - Scale exposure each day:  
     `position_t = signal_t * (target_vol / realized_vol_t)`
   - Cap leverage to avoid excessive exposure in calm regimes

5. **Regime Adjustment**
   - Reduce exposure in high-volatility regimes (e.g. half-weight or flat)
   - Maintain full exposure in low-volatility regimes

6. **Backtesting**
   - Compute daily strategy returns:  
     `strategy_return_t = position_{t-1} * asset_return_t - transaction_costs`
   - Evaluate cumulative performance and risk-adjusted metrics.

---

## Performance Metrics

- Annualized Return  
- Annualized Volatility  
- Sharpe Ratio  
- Maximum Drawdown  
- Cumulative Return  
- Regime-wise performance breakdown

---

## File Structure

regime_trend_vol_project/
│
├── src/
│ ├── data.py
│ ├── signals.py
│ ├── regime.py
│ ├── vol_target.py
│ ├── backtest.py
│ └── utils.py
│
├── notebooks/
│ └── main_notebook.ipynb
│
├── data/
│ └── prices.csv
│
├── results/
│ ├── equity_curve.png
│ ├── metrics_table.csv
│ └── regime_plot.png
│
├── requirements.txt
└── README.md

---

## Dependencies

- Python 3.10+
- pandas  
- numpy  
- matplotlib  
- yfinance  
- (optional) hmmlearn

Install all dependencies with:
pip install -r requirements.txt

yaml
Copy code
