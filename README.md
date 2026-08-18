# ERCOT DART Machine Learning Trading Strategy

A machine learning framework for modeling **ERCOT Day-Ahead vs. Real-Time (DART) electricity price spreads** using power market fundamentals, weather, renewable generation, and natural gas data.

This project was developed as part of the **Texas A&M Trading, Risk & Investments Program (TRIP)** to explore whether fundamental market information can identify systematic opportunities created by differences between Day-Ahead expectations and Real-Time market outcomes.

## Project Overview

ERCOT's Day-Ahead Market reflects expectations for system conditions before the operating day, while Real-Time prices reflect actual system conditions as they occur. Differences between forecasts and realized conditions—including load, renewable generation, weather, fuel prices, and transmission conditions—can create significant DART price spreads.

This project uses **LightGBM gradient-boosted decision trees** to model those relationships and evaluate whether they contain useful predictive information.

Two separate modeling problems are considered:

* **Direction:** Predict whether the DART spread will be positive or negative.
* **Magnitude:** Estimate the expected size of the spread.

## Data & Features

The model incorporates hourly market and fundamental variables including:

* Day-Ahead and Real-Time electricity prices
* System load
* Wind generation
* Solar generation
* Net load
* Natural gas prices
* Temperature and weather variables
* Lagged DART spreads
* Lagged fundamental variables
* Rolling volatility and moving averages
* Calendar variables including hour, day, and month

Data was sourced primarily from **ERCOT and the U.S. Energy Information Administration (EIA)**.

## Methodology

The strategy uses **LightGBM**, a gradient-boosted decision-tree framework capable of modeling nonlinear relationships and interactions between market variables.

To evaluate performance outside the training sample, the models were tested using chronological train/test splits rather than randomized observations.

The primary specification was:

**Training Period:** 2022–2024
**Out-of-Sample Test:** 2025

An additional robustness test trained the models on **2022–2023** data and evaluated performance on **2024**.

This structure was designed to test whether relationships learned during previous market regimes generalized to future, unseen market conditions.

## Key Results

The models demonstrated predictive information out of sample across multiple testing periods.

For the magnitude model, the 2025 out-of-sample test produced approximately:

* **RMSE:** 41.07
* **Realized / Predicted Correlation:** 0.316

The broader research suggests that combining physical power-market fundamentals with machine learning can identify nonlinear relationships associated with DART spread behavior.

## Important Limitations

This project is a **research backtest rather than an immediately deployable trading system**.

Most importantly, the simulation assumes that Day-Ahead orders are cleared. ERCOT's Day-Ahead Market operates as an auction, meaning actual trading performance depends on bid prices, clearing probabilities, liquidity, transaction costs, and market impact.

The current model therefore evaluates **predictive signal quality and theoretical strategy performance**, rather than perfectly replicating executable market returns.

Future research could incorporate:

* ERCOT Day-Ahead auction mechanics and clearing probabilities
* More granular 15-minute market data
* Transmission congestion and nodal information
* Improved position sizing and risk management
* Additional regime-dependent modeling
* Probabilistic forecasts rather than point estimates

## Repository Contents

* **Jupyter Notebook** — Data processing, feature engineering, model training, backtesting, and analysis
* **Dataset** — Data used to construct model features and evaluate the strategy
* **Research Paper** — Original paper documenting the motivation, methodology, results, and conclusions

## Tools & Technologies

**Python** · **pandas** · **NumPy** · **LightGBM** · **statsmodels** · **Matplotlib** · **Jupyter Notebook**

---

**Jack Usner**
Texas A&M University
Trading, Risk & Investments Program (TRIP)
Finance | Texas A&M Men's Golf
