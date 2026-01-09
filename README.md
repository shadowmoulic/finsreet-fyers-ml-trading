# ML-Driven Trading Strategy using FYERS API

This repository contains a **fully automated, end-to-end machine learning trading system** developed for **KSHITIJ 2026 – AQUA (FYRES Presents)** by the Finance & Economics Club, IIT Kharagpur.

The project demonstrates the complete pipeline:

> **Market Data → Feature Engineering → ML Model → Trade Signals → Backtesting → Deployment-ready Execution**

The emphasis is on **methodological rigor, reproducibility, and risk control**, rather than raw profit maximization.

* * *

## Project Overview

*   **Stock:** RITES Ltd (RITES.NS)
    
*   **Market:** NSE (Daily OHLCV)
    
*   **Data Window:** 1 Nov 2025 – 31 Dec 2025
    
*   **Model:** Logistic Regression (probabilistic classification)
    
*   **Prediction Horizon:** Next trading day direction
    
*   **Deployment Output:** Trade signals for Jan 1–8
    

The strategy predicts the **probability of an upward price move** and converts it into systematic trading decisions.

* * *

## Repository Structure

`. ├── data/ │   └── RITES.csv              # Historical daily OHLCV data │ ├── strategy_pipeline.py       # End-to-end ML trading pipeline │ └── README.md                  # Project documentation`

* * *

## Methodology Summary

### 1\. Feature Engineering

All features are derived strictly from OHLCV data:

*   SMA (20), EMA (20) – trend
    
*   RSI (14) – momentum
    
*   MACD & signal line – trend strength
    
*   Bollinger Bands – volatility
    

### 2\. Model

*   Logistic Regression classifier
    
*   Outputs probability of next-day upward movement
    
*   Scaled features using `StandardScaler`
    
*   Class balancing to handle skewed data
    

### 3\. Trading Logic

*   **LONG:** Probability ≥ 0.65
    
*   **SHORT:** Probability ≤ 0.35
    
*   **NO TRADE:** Otherwise
    

This confidence-based approach reduces overtrading and noisy signals.

### 4\. Risk Management

*   Fixed risk per trade
    
*   No trades on zero-volume days
    
*   No manual intervention at any stage
    

* * *

## Backtesting Approach

A **strict walk-forward backtest** is applied:

*   **Training Period:** 3 Nov 2025 – 10 Dec 2025
    
*   **Testing Period:** 11 Dec 2025 – 31 Dec 2025
    

Metrics evaluated:

*   Total Return
    
*   Maximum Drawdown
    
*   Sharpe Ratio
    

This ensures realistic evaluation without look-ahead bias.

* * *

## Jan 1–8 Signal Generation

After completing backtesting, the model is **frozen** and used to generate **deployment signals for the next 5 trading days (Jan 1–8)** using only data available up to Dec 31.

No retraining or parameter tuning is performed during deployment.

* * *

## FYERS API Integration

The strategy is designed to integrate directly with the **FYERS Trading API** for:

*   Historical market data fetching
    
*   Automated market order execution
    

Trade execution logic maps model signals to FYERS API orders:

*   LONG → Buy order
    
*   SHORT → Sell order
    
*   NO TRADE → No action
    

* * *

## How to Run the Project

### 1\. Install Dependencies

`pip install pandas numpy scikit-learn`

### 2\. Run the Pipeline

`python strategy_pipeline.py`

The script will:

*   Train the model
    
*   Perform walk-forward backtesting
    
*   Print performance metrics
    
*   Generate trade signals for Jan 1–8
    

* * *

## Assumptions & Limitations

*   Daily close-to-close execution
    
*   No transaction cost or slippage modeling
    
*   Short historical data window
    
*   Single-asset strategy
    

These limitations are acknowledged to maintain clarity, transparency, and rule compliance.

* * *

## Conclusion

This repository presents a **clean, reproducible ML-based trading system** integrated with the FYERS ecosystem.  
The project focuses on **disciplined system design, probabilistic decision-making, and realistic trading constraints**, in line with the objectives of the competition.

* * *

### 📌 Note

This project is intended for academic and competition purposes only and does not constitute financial advice.
