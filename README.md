# 📈 Technical Trading Strategies

This repository contains implementations of various **technical trading strategies** using Python and pandas-based backtesting logic. These strategies are designed to help explore, evaluate, and build systematic models based on market behavior and price/volume indicators.

> ✅ Currently implemented:
- **Volume Reversal Strategy** (explained below)

> 🚧 Coming soon:  
Momentum-based strategies, mean reversion, moving average crossovers, breakout systems, and machine learning-based models.

---

## 🔁 Volume Reversal Strategy

The **Volume Reversal Strategy** aims to detect short-term trend reversals by analyzing:
- Price volatility over the past 5 days
- A drop in recent volume compared to earlier volume
- Direction of the recent price move

### Strategy Conditions

**Buy Signal:**
- `|5-day price change| > 100-day rolling std dev of price change`
- `5-day average volume < 5-10 day lagged average volume`
- `5-day price change < 0` (i.e. price has dropped)

**Sell Signal:**
- Same as above, but `5-day price change > 0` (i.e. price has risen)

The position is **held for 5 days** unless a counter signal appears earlier.

---

## 🛠 Implementation Overview

- **Data:** AAPL stock (2018–2019), loaded from CSV
- **Libraries:** `pandas`, `numpy`, `matplotlib`
- **Signal logic:** Based on rolling window features (`rolling.mean`, `rolling.std`)
- **Execution logic:** Signals are stored, evaluated over time, and translated into position-holding days using `c_signal` and `exit` columns
- **Returns:** Calculated both for the strategy and the market
- **Sharpe Ratio:** Used to evaluate performance vs baseline

---

## 📉 Sample Output

| Date       | Close | Signal | c_signal | exit | Strategy Return | Market Return |
|------------|--------|--------|----------|------|------------------|----------------|
| 2019-06-11 | 194.81 |   -1   |   -1     | -1   |       ...        |      ...       |
| 2019-06-14 | 192.74 |   -1   |   -1     | -4   |       ...        |      ...       |
| ...        |  ...   |  ...   |   ...    | ...  |       ...        |      ...       |

---

### 📊 Performance Visualization

The notebook plots cumulative returns of both the market and the strategy after the 100-day warmup period:

- 📈 Green line: Strategy returns
- 📉 Red line: Market returns

This visualizes periods where the strategy outperforms or underperforms the baseline.

---

### 🧠 Sharpe Ratio

This strategy underperformed with sharpe of -0.2. Will be working on some improvements.
