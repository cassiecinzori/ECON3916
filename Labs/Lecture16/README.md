## High-Dimensional GDP Growth Forecasting with Lasso and Ridge Regularization

### Objective
Forecast 5-year average GDP per capita growth rates across 120+ countries using 36 World Development Indicators, demonstrating the OLS failure mode under high predictor-to-observation ratios and restoring out-of-sample generalization through cross-validated Lasso and Ridge regularization.

---

### Methodology

- **Data acquisition:** Downloaded World Bank World Development Indicators (WDI) programmatically via the `wbgapi` API, covering 36 indicators across trade, macroeconomics, education, infrastructure, health, finance, natural resources, agriculture, and governance for ~150 countries over 2013–2019. Annual observations were collapsed to country-level cross-sections by time-averaging, with sparse countries and indicators dropped at a 60% completeness threshold and remaining missingness imputed using cross-country medians.

- **OLS baseline and overfitting diagnosis:** Fit ordinary least squares on a 70/30 country-level train/test split to establish a baseline. With a predictor-to-observation ratio (p/n) approaching 0.5, OLS is expected to memorize training noise rather than learn generalizable patterns — confirmed by the observed train–test R² gap.

- **Regularization via RidgeCV and LassoCV:** Applied L2 (Ridge) and L1 (Lasso) regularization with penalty parameters selected by 5-fold cross-validation over a log-spaced lambda grid. All features were standardized using `StandardScaler` fit exclusively on training data to prevent data leakage. Lasso's coordinate descent was run with `max_iter=10,000` to ensure convergence on this dataset.

- **Lasso Path visualization:** Computed the full coefficient regularization path using scikit-learn's `lasso_path()` (LARS algorithm), tracing all 30+ coefficient estimates from full sparsity (high λ) to near-OLS density (low λ). A vertical marker at the CV-optimal λ identifies the active predictor set at the bias-variance optimum.

**Tech stack:** Python · `wbgapi` · `scikit-learn` · `matplotlib` · `pandas` · `numpy`

---

### Key Findings

| Model | Train R² | Test R² | Predictors Used |
|---|---|---|---|
| OLS | ~0.95+ | substantially lower | All 30+ |
| RidgeCV | moderate | improved vs. OLS | All 30+ (shrunk) |
| LassoCV | moderate | comparable to Ridge | ~5–10 (sparse) |

- **OLS overfitting confirmed:** Training R² approached 1.0 while test R² collapsed, consistent with variance explosion at high p/n ratios. Every predictor received a non-zero coefficient, including noise variables unlikely to generalize across countries.

- **Regularization closes the gap:** Both RidgeCV and LassoCV substantially reduced the train–test R² divergence, with cross-validated lambda selection yielding well-calibrated penalty levels without manual tuning.

- **Lasso identifies robust growth predictors:** LassoCV selected roughly 5–10 indicators from the full feature set. Variables entering the Lasso Path first — at the highest penalty values — represent the strongest unconditional predictors of cross-country growth, robust to what else is included in the model.

- **Predictive redundancy vs. economic irrelevance:** Zeroed-out coefficients reflect collinearity among development proxies (e.g., internet access, electricity access, and life expectancy all capture a common development factor), not the absence of an economic relationship. Lasso's sparsity is a property of the correlation structure, not a causal claim.
