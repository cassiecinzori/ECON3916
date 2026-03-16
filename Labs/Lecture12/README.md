# Architecting the Prediction Engine: OLS, Hedonic Pricing & RMSE Evaluation

## Objective
Architect a multivariate Ordinary Least Squares prediction engine on cross-sectional real estate data to shift the analytical frame from causal parameter estimation toward out-of-sample loss minimization, quantifying algorithmic pricing risk in actionable financial terms.

## Data
**Zillow ZHVI 2026 Micro Dataset** — contemporary cross-sectional residential real estate valuations with structural and locational property features.

## Methodology
- **Environment & Ingestion:** Loaded the Zillow dataset into a pandas DataFrame and conducted exploratory data analysis to characterize the scale and variance of the target variable, `Home_Value`.
- **Model Architecture:** Specified a hedonic pricing model using the `statsmodels` Patsy Formula API, regressing `Home_Value` on `Square_Footage`, `Property_Age`, and `Distance_to_Transit` — feature selection grounded in economic theory of property valuation.
- **Model Fitting & Diagnostics:** Fit the OLS model via the normal equations; interrogated the regression summary for coefficient sign consistency with economic intuition (depreciation effects, transit accessibility premia) and t-statistic significance.
- **Prediction Generation:** Applied the estimated parameter vector β̂ to the feature matrix to produce a continuous vector of fitted valuations, pivoting the workflow from explanatory inference to predictive output.
- **Loss Quantification:** Computed Root Mean Squared Error (RMSE) using `statsmodels.tools.eval_measures`, converting model error from an abstract statistical metric into a real US Dollar figure representing the algorithm's financial blind spot.

## Key Findings
Successfully operationalized the transition from classical econometric explanation to predictive engineering within a production-relevant real estate pricing context. By expressing model error as RMSE in US Dollars rather than dimensionless fit statistics, the analysis yields a directly interpretable measure of algorithmic business risk — the average dollar magnitude by which the model would misprice an asset. This reframing exposes a critical limitation of R² as a standalone performance benchmark: a model can exhibit strong explanatory fit while carrying an RMSE large enough to produce materially adverse acquisition or disposition decisions in a live market.

## Tools & Libraries
`Python` · `pandas` · `NumPy` · `statsmodels` (Formula API / Patsy) · `Plotly`
