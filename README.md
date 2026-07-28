# Target Corporation Quarterly Revenue Forecasting

A time-series regression project that models Target Corporation's quarterly revenue using a linear trend combined with seasonal dummy variables, then evaluates forecast accuracy against actual results.

## Overview

Retail revenue is strongly seasonal — Q4 spikes with holiday spending, and Q1 typically dips afterward. This project builds an OLS regression model that separates the underlying long-term growth trend from these recurring seasonal effects, then uses the model to predict quarterly revenue and assess how well those predictions hold up against actual performance.

## Business Context

The analysis is framed as a memo from an equity research team ("QuantFolio Solutions") to a wealth management client evaluating a potential investment in Target. The goal is to explain revenue growth and seasonality in plain terms that support an investment decision.

## Data

- **Source:** Quarterly sales data (`qSales_2024.csv`) filtered to Target Corporation (ticker: `TGT`)
- **Period:** 2000 Q4 – 2023 Q4 (93 quarterly observations)
- **Key fields:** report date, fiscal quarter, quarterly revenue (`saleq`)

## Methodology

1. **Data preparation** — filtered the dataset to Target, sorted chronologically, and created a sequential `Time` index to capture the long-run trend.
2. **Seasonal features** — engineered dummy variables for fiscal Q1 (`Q1`) and Q4 (`Q4`), using Q2/Q3 as the baseline period.
3. **Model** — fit an OLS regression:

   `Revenue = β₀ + β₁(Time) + β₂(Q1) + β₃(Q4) + ε`

4. **Evaluation** — generated in-sample predictions and compared them visually and statistically against actual revenue, using MAPE to quantify average forecast error.

## Key Findings

- **Q4 effect:** Holiday-quarter revenue runs roughly $4.4B higher than a typical Q2/Q3 quarter, holding the trend constant.
- **Q1 effect:** Post-holiday revenue comes in about $233M lower than the Q2/Q3 baseline.
- **Fit:** The model explains ~89.5% of the variation in quarterly revenue (R²).
- **Forecast accuracy:** Testing MAPE of ~12%, meaning predictions typically differ from actual revenue by about 12%.
- **Caveat:** Actual revenue grew faster than the model predicted in later years, suggesting the linear trend may understate recent acceleration — a reminder that seasonality explains variation around the trend, not the strength of the trend itself.

## Tools & Libraries

- Python
- `pandas`, `numpy` — data wrangling
- `statsmodels` — OLS regression
- `matplotlib` — visualization

## Repository Contents

| File | Description |
|---|---|
| `w11_quiz.ipynb` | Full analysis notebook: data prep, model fitting, evaluation, and client memo |
| `w11_quiz.pdf` | PDF export of the notebook for quick viewing without running code |

## How to Run

```bash
pip install pandas numpy matplotlib statsmodels
jupyter notebook w11_quiz.ipynb
```

Place `qSales_2024.csv` in the same directory before running.

## Notes

This project was completed as part of a business analytics course exercise and is included here to demonstrate applied regression modeling, seasonal decomposition, and translating statistical results into a client-facing recommendation.
