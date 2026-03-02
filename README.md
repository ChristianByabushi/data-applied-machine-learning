# Financial Understanding of DJIA Component Companies

> **Course:** DIAML — Assignment 5  
> **Topics:** PCA · Hierarchical Clustering · Time Series Forecasting

---

## Overview

This project applies unsupervised learning and time series techniques to analyze all **30 Dow Jones Industrial Average (DJIA)** stocks over a 3-year period (2022–2024). The goal is to uncover market structure, sector groupings, and forecast future stock prices using classical and deep learning models.

---

## Project Structure

```
├── financial_pca.ipynb   # Main notebook
├── correlation_heatmap.png       # Pearson correlation heatmap
└── README.md
```

---

## Questions Covered

### Q1 — Principal Component Analysis (PCA)
- Downloaded 3 years of daily closing prices for all 30 DJIA tickers via `yfinance`
- Computed **daily log returns** and the **Pearson correlation matrix**
- Applied PCA on standardized returns:
  - **PC1** (~34% variance) — confirmed as a broad **market factor** (all 30 stocks have positive loadings)
  - **PC2** — captures a **Growth vs. Defensive** contrast (Tech vs. Consumer Staples/Energy)
- Determined that **~20 components** are needed to preserve 95% of variance, indicating moderate market fragmentation

### Q2 — Hierarchical Clustering
- Applied **matrix seriation** to reorder the correlation matrix, revealing a **block-diagonal** sector structure
- Built a **hierarchically clustered heatmap** (clustermap) using Agglomerative Clustering
- Identified **4 clusters**:
  | Cluster | Composition | Characteristics |
  |---------|-------------|-----------------|
  | 1 | Financials & Cyclicals (GS, JPM, AXP) | High market beta, rate-sensitive |
  | 2 | Technology & Growth (MSFT, AAPL, NVDA, AMZN) | High PC2 loading, risk-on |
  | 3 | Defensives & Consumer Staples (KO, PG, JNJ) | Low beta, risk-off |
  | 4 | Mixed Value | Moderate loadings across factors |

### Q3 — Time Series Forecasting (Procter & Gamble)
- Used **PG** (oldest continuous DJIA member, since 1932) on monthly prices
- Performed **ADF stationarity tests** → confirmed d=1 differencing needed
- **STL decomposition** revealed a strong trend with weak-to-moderate seasonality
- Trained and compared four models:
  - Simple Moving Average (baseline)
  - ARIMA(1,1,1)
  - SARIMA (with seasonal terms)
  - LSTM (neural network)
- Evaluation metrics: **MAE** and **RMSE**

---

## Tech Stack

| Library | Usage |
|---------|-------|
| `yfinance` | Stock data download |
| `pandas` / `numpy` | Data manipulation |
| `scikit-learn` | PCA, scaling, clustering |
| `scipy` | Hierarchical clustering, dendrograms |
| `statsmodels` | ARIMA, SARIMA, ADF test, STL |
| `matplotlib` / `seaborn` | Visualization |
| `PyTorch` / `Keras` | LSTM forecasting |

---

## Key Findings

- **Market integration is moderate**: PC1 explains ~34% of variance, but ~20 PCs are needed for 95% — diversification within DJIA is meaningful.
- **Sector structure is real**: Clustering clearly recovers Tech, Financials, and Defensives without using any sector labels.
- **ARIMA/SARIMA outperforms LSTM** on monthly financial data due to limited sample size and the strong trend captured by differencing.

---

## How to Run

```bash
# Clone the repo
[git clone https://github.com/cbyabush/<repo-name>.git](https://github.com/ChristianByabushi/data-applied-machine-learning)
cd <repo-name>

# Install dependencies
pip install yfinance pandas numpy scikit-learn scipy statsmodels matplotlib seaborn

# Launch notebook
jupyter notebook cbyabush_assignment_5.ipynb
```

---

## License

This project is for academic purposes — DIAML course, 2024.﻿# data-applied-machine-learning


