# Systematic DA/RT Trading Strategy in ERCOT

**Jack Usner | Texas A&M University**

This repository contains the research paper, Python analysis, and dataset supporting my systematic trading strategy for the ERCOT Day-Ahead/Real-Time (DA/RT) power market.

## Project Overview

This project investigates whether conditional inefficiencies in ERCOT DA/RT power spreads can be identified using machine learning and physical power-market fundamentals.

I developed two **LightGBM** models to estimate:

* **Spread magnitude** — when large DA/RT price deviations are likely to occur
* **Spread direction** — whether Real-Time prices are expected to settle above or below Day-Ahead prices

The models incorporate power-market, weather, renewable generation, load, natural gas, and engineered time-series features. Trading signals are generated only when both predicted spread magnitude and directional conviction are sufficiently high.

The strategy also incorporates **maximum-drawdown and rolling-loss risk controls** and is evaluated using chronological out-of-sample backtests.

## Repository Contents

### Python Analysis

**ERCOT DA/RT Machine Learning & Systematic Trading Strategy**

The Jupyter notebook contains the complete quantitative workflow, including:

* Data preparation and feature engineering
* LightGBM model construction
* Spread magnitude and directional prediction
* Out-of-sample model evaluation
* Trading signal construction
* Risk-management implementation
* Transaction-cost analysis
* Backtesting and performance visualization

The notebook has been saved with its executed outputs, allowing the model results, statistics, and visualizations to be reviewed directly on GitHub.

### Dataset

**ERCOT Power Market Dataset | 2022–2025**

The CSV dataset used by the notebook combines:

* ERCOT Day-Ahead and Real-Time electricity prices
* ERCOT system load
* Texas solar generation
* Houston-area temperature, wind speed, and cloud coverage
* Henry Hub natural gas prices
* Engineered market and time-series variables

The original market data was standardized to an hourly framework for modeling.

### Research Paper

**Systematic DA/RT Trading Strategy**

The accompanying paper explains the market rationale, modeling methodology, trading rules, risk-management framework, out-of-sample results, and limitations of the strategy.

## Out-of-Sample Results

The models and trading framework were evaluated across two separate chronological out-of-sample periods:

**2025 Backtest**

* Magnitude-model correlation: **0.316**
* Directional-model correlation: **0.155**
* Annualized Sharpe after estimated transaction costs: **3.25**
* Maximum drawdown after estimated transaction costs: **-$361.95/MW**

**2024 Robustness Backtest**

* Models retrained using 2022–2023 data
* Magnitude-model correlation: **0.372**
* Directional-model correlation: **0.181**
* Annualized Sharpe after estimated transaction costs: **2.76**
* Maximum drawdown after estimated transaction costs: **-$374.58/MW**

The consistency across separate out-of-sample periods provides evidence that the identified relationships are not isolated to a single test year.

## Risk Management

The strategy evaluates multiple risk-management configurations:

* Baseline strategy
* Maximum-drawdown stop
* Rolling 24-hour loss filter
* Combined drawdown and rolling-loss controls

The combined framework substantially reduced maximum drawdown in both out-of-sample backtests while maintaining the strategy's underlying signal.

## Key Limitations

This project is a research backtest rather than a directly deployable trading system. Important limitations include:

* Day-Ahead auction bid and order-clearing dynamics are not modeled
* Hourly average prices abstract from higher-frequency market behavior
* Some model inputs may not be known perfectly at the time of execution
* Market impact and bid-ask effects are not explicitly modeled
* Transaction costs are represented using a fixed estimate

These limitations provide potential directions for extending the research toward a more realistic implementation.

## Tools & Technologies

**Python · pandas · NumPy · LightGBM · scikit-learn · Matplotlib · JupyterLab**

## Data Sources

**ERCOT · U.S. Energy Information Administration (EIA) · Open-Meteo Weather API**

---

*This project was developed for academic research and educational purposes and does not represent live trading performance or investment advice.*
