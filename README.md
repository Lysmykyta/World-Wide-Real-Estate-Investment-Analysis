## Time Series Revenue Forecasting with Python

This repository contains a Python workflow (adapted from an AFM244 Week 11 quiz notebook) that demonstrates how to build and evaluate time-series forecasting models for quarterly company revenues using regression techniques.

## Project Overview

The project focuses on:

- Exploring quarterly revenue data for:
  - **Apple (AAPL)**
  - **Target (TGT)**
- Building baseline time-trend regression models
- Enhancing models with **dummy variables** and **interaction terms** to capture seasonal or event-driven effects (e.g., Q1 or Q4 effects)
- Evaluating forecast performance on a hold-out testing set
- Generating **prediction intervals** for forecasts

The workflow is designed as an educational example for time-series forecasting and regression modeling.

---

## Key Features

- **Data Loading & Preparation**
  - Reads quarterly revenue data from `qSales_2024.csv`
  - Filters data for specific tickers (AAPL, TGT)
  - Ensures dates are properly handled for plotting
  - Creates a numerical `time` index (1, 2, 3, …) for regression

- **Visualization**
  - Line plots of revenue over time for exploratory analysis

- **Baseline Time-Trend Regression**
  - Uses `statsmodels` OLS:
    - `revenue = β₀ + β₁ * time`
  - Trains on **75%** of the data
  - Tests on the remaining **25%**

- **Forecast Intervals**
  - Uses `model.get_prediction(...).summary_frame(alpha=...)` to generate:
    - Predicted mean revenue
    - Observation-level lower/upper bounds (e.g., 80% confidence)

- **Dummy Variable and Interaction Model**
  - Creates quarterly dummy variables, e.g.:
    - Apple example: `release_dummy_variable` for **Q1**
    - Target example: `release_dummy_variable` for **Q4**
  - Interaction term:
    - `release_dummy_interaction = time * release_dummy_variable`
  - Extended model:
    - `revenue = β₀ + β₁ * time + β₂ * dummy + β₃ * (time * dummy)`
  - Re-trains and evaluates improved models

- **Performance Evaluation (Target Example)**
  - Computes **MAPE** (Mean Absolute Percentage Error) on testing data:
    - Adds `rev_predicted` and `abs_pct_error` columns
    - Reports average MAPE (e.g., ~12%)
  - Plots:
    - Actual versus predicted testing revenues with dummy-variable model

- **Synthetic Forecasting**
  - Loads `synthetic_data.csv` to forecast **future** revenue beyond the observed sample using the fitted model.

---

## Files

- `Copy of AFM244_S26_Week11_Quiz.ipynb` (or `.py`)
  - Main analysis script / notebook:
    - Data loading
    - Visualization
    - Model training and testing
    - Forecasting and evaluation

- `qSales_2024.csv`
  - Quarterly revenue data for multiple tickers (AAPL, TGT, etc.).
  - Must include:
    - `tic` (ticker)
    - `datadate` (date)
    - `saleq` (quarterly sales / revenue)
    - `fqtr` (fiscal quarter)

- `synthetic_data.csv`
  - Synthetic time periods and dummy variables used for out-of-sample forecasting.

> Note: CSV filenames and column names must match those used in the script.

---

## Requirements

Install dependencies using `pip`:

```bash
pip install pandas numpy statsmodels matplotlib
