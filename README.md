# ECO6130 Group 8 — Robustness & Regime: ML in Volatility Trading

Course: ECO6130 Final Project, Spring 2026
Group members: Li Shangze (225020302), Shan Xintong (225020340), Chen Liuyan (225020342), Sun Yihui (225020345), Wen Huiming (225020362)

Final report: see `ECO6130_Group8_Final_Report.docx`.
Presentation deck: see `presentation.pptx`.
Runnable code: see `etf_cross_sectional_strategy.ipynb`.

## Overview

This project implements a **Robustness and Regime-Aware Cross-Sectional ETF Ranking** system 
that predicts 5-day forward returns for 41 ETFs across multiple asset classes, constructs 
long-short portfolios based on model predictions, and applies volatility scaling for risk control.

## Key Results

| Metric | Value |
|--------|-------|
| Annualized Return | **26.26%** |
| Annualized Volatility | **16.08%** |
| Sharpe Ratio | **1.633** |
| Maximum Drawdown | **32.5%** |
| Calmar Ratio | **0.807** |

## Critical Finding: Signal Inversion

The model's predictions have a negative correlation with actual returns (IC ≈ -0.009), 
indicating the model learned a **contrarian/reversal signal**. Signal inversion is required 
for deployment:

| Signal Direction | Sharpe Ratio | Ann Return |
|-----------------|-------------|------------|
| Normal Signal | -2.531 | -40.56% |
| **Inverted Signal** | **+1.633** | **+26.26%** |

## Files

| File | Description |
|------|-------------|
| `etf_cross_sectional_strategy.ipynb` | Complete Jupyter notebook with all code |
| `etf_strategy_backtest.csv` | Daily backtest results (returns, cumulative value) |
| `etf_predictions.csv` | Cross-sectional predictions for all ETFs |
| `panel_enhanced.csv` | Enhanced feature panel (20 features, 78K rows) |
| `strategy_analysis.png` | Cumulative returns, drawdown, spread distribution |
| `ic_distribution.png` | Daily IC distribution |
| `final_report.md` | Detailed performance report |

## Data

**Input**: `unified_etf_data.csv` (46 ETFs, 2010-2026)
**ETF Universe**: 41 tradeable ETFs covering equity, bond, commodity, REIT, 
international, sector, and factor classes.

## Methodology

### Feature Engineering (20 features)
- **Return features**: 5d, 10d, 20d, 60d momentum
- **Volatility features**: 20d vol, vol z-score, HAR-RV (daily/weekly/monthly)
- **Technical indicators**: RSI-14, MACD histogram, price position
- **Volume features**: Volume z-score, volume trend
- **Macro features**: VIXM level, credit spread, term spread, SPY momentum
- **Cross-sectional**: Sector average momentum/volatility

### Models
- **CatBoost** (primary): 200 iterations, depth=6, learning_rate=0.08
- **HAR-RV**: Baseline using realized volatility features only
- **ElasticNet**: L1/L2 regularized linear model
- **GradientBoosting**: 100 estimators, max_depth=3

### Backtest Configuration
- Walk-forward: 756-day train / 378-day test steps
- Transaction cost: 5bp per side (10bp round-trip)
- Volatility scaling: 63-day rolling window, 15% annual target
- Position sizing: Top/bottom decile equal-weight

## Setup & Execution

### Requirements
```bash
pip install pandas numpy matplotlib seaborn scikit-learn scipy catboost hmmlearn torch
```

### Run
```bash
jupyter notebook etf_cross_sectional_strategy.ipynb
```

## Authors
Quantitative Research Project - Cross-Sectional ETF Ranking Strategy v2
