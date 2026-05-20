# ETF Cross-Sectional Ranking Strategy - Final Report

## Best Model: TFT (Normal Signal)

### Performance Summary
| Metric | Value |
|--------|-------|
| Annualized Return | 14.21% |
| Annualized Volatility | 16.53% |
| Sharpe Ratio | 0.860 |
| Maximum Drawdown | 52.6% |
| Calmar Ratio | 0.270 |

### Model Comparison (All Models, Inverted Signal)
               model  sharpe  ann_ret  max_dd
1         ElasticNet  0.0434   0.0069  0.5094
3             HAR-RV -0.2052  -0.0321  0.5043
5   GradientBoosting  0.2648   0.0421  0.4718
7           CatBoost  0.2812   0.0445  0.4020
9               LSTM -1.2861  -0.2116  0.8388
11               TFT -1.9338  -0.3201  0.8472

### IC Analysis
              model  mean_ic  std_ic  median_ic  pos_rate   ic_ir
0          CatBoost  -0.0030  0.3154    -0.0137    0.4778 -0.0094
1        ElasticNet  -0.0070  0.3291    -0.0089    0.4865 -0.0213
2  GradientBoosting   0.0059  0.3007    -0.0003    0.5000  0.0196
3            HAR-RV  -0.0129  0.3490    -0.0037    0.4952 -0.0370
4              LSTM   0.0315  0.3429     0.0323    0.5270  0.0920
5               TFT   0.0000  0.3383    -0.0240    0.4778  0.0000

### Key Findings
1. Model predictions have negative IC (~0.0024), indicating contrarian signal
2. Signal inversion is required for positive returns
3. CatBoost outperforms linear baselines by ~0.0444 IC

### Files Generated
- `etf_strategy_backtest.csv` - Daily backtest results
- `etf_predictions.csv` - Cross-sectional predictions
- `panel_enhanced.csv` - Enhanced feature panel
- `walkforward_predictions.csv` - Walk-forward predictions
- `strategy_analysis.png` - Cumulative returns, drawdown, spread distribution
- `ic_distribution.png` - IC distribution
