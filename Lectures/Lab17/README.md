# NY Fed Yield Curve Recession Model Replication
 
**Objective:** Replicated the Federal Reserve Bank of New York's yield curve recession probability model using logistic regression on FRED macroeconomic data to forecast NBER-defined recessions 12 months ahead.
 
## Methodology
- Retrieved daily T10Y3M (10Y–3M Treasury yield spread) and monthly USREC (NBER recession indicator) from FRED via API, resampling the spread to month-end and applying a 12-month lag to align with the NY Fed's forward-looking specification
- Benchmarked a Linear Probability Model (OLS) against logistic regression to document LPM failure modes on a real binary outcome
- Fitted a logistic regression using scikit-learn and extracted the yield spread odds ratio with 95% confidence intervals via statsmodels
- Generated a full recession probability time series from 1970 to present, replicating the NY Fed's published chart format with NBER recession shading
 
## Key Findings
The LPM produced logically impossible predicted probabilities on 16% of observations, confirming the practical case for logistic regression on binary outcomes. The fitted model estimated a yield spread odds ratio of 0.45 (95% CI: 0.33–0.60), meaning each 1 percentage-point steepening of the curve reduces recession odds by approximately 55%. The model assigned peak recession probabilities of ~43% during the 2022–2024 inversion — the longest since the 1980s — yet no NBER recession materialized, illustrating that elevated probabilistic forecasts are not equivalent to definitive predictions and should be interpreted in the context of the full distribution of outcomes.
 
## Tech Stack
`Python` `pandas` `numpy` `scikit-learn` `statsmodels` `matplotlib` `fredapi`
 
