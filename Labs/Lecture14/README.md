## AI Capex Diagnostic Modeling

**Objective:** Applied structural integrity auditing to an OLS regression model predicting AI Software Revenue from 2026 Nvidia capital expenditure and deployment data, diagnosing and correcting Gauss-Markov violations to eliminate false statistical confidence.

**Methodology:**
- Constructed a naive OLS baseline model using hardware capex, data center power, and cloud GPU deployment metrics as predictors, documenting the deceptively high R² and artificially low p-values
- Performed visual residual forensics by plotting residuals against fitted values, identifying a pronounced cone-shaped fan pattern indicative of heteroscedasticity scaling with capital expenditure tier
- Formalized the diagnosis via the White Test, statistically confirming non-constant error variance across the predictor space
- Calculated Variance Inflation Factors (VIF) for all predictors to audit multicollinearity, using a design matrix with an explicit intercept column to ensure mathematically valid scores
- Applied HC3 Heteroscedasticity-Consistent standard errors to re-fit the model, correcting the covariance matrix without altering the underlying coefficient estimates

**Key Findings:** The naive OLS model exhibited severe heteroscedasticity concentrated at high capital expenditure tiers, where error variance expanded significantly with predicted revenue — a structural failure that artificially compressed standard errors and produced misleading p-values. Applying HC3 robust estimation appropriately widened confidence intervals, revealing the true, conservative significance thresholds of the deployment metrics. Variables that appeared highly significant under naive OLS lost statistical credibility post-correction, underscoring the risk of drawing inference from unaudited regression output in high-dimensional, stochastic environments.

**Tools:** Python, pandas, statsmodels, matplotlib, seaborn
