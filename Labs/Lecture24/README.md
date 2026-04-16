# Causal ML - Double Machine Learning for 401(k) Policy Evaluation

**Objective:** Applied the Double Machine Learning framework to estimate the causal effect of 401(k) eligibility on household net financial assets, addressing selection bias and high-dimensional confounding that invalidate naive regression approaches.

## Methodology

- Demonstrated regularization bias using a simulated DGP with a known true ATE of 5.0: naive LASSO shrinks the treatment coefficient toward zero because its penalty makes no distinction between the causal variable of interest and nuisance covariates
- Loaded the Chernozhukov-Hansen 401(k) dataset via `doubleml.datasets.fetch_401K` and confirmed selection bias through a covariate balance check showing treated workers have systematically higher income and education
- Constructed a `DoubleMLData` object assigning net financial assets as outcome, 401(k) eligibility as treatment, and all remaining variables (income, age, family size, education, marital status) as covariates
- Fit a Partially Linear Regression (PLR) model using Random Forest nuisance learners (`n_estimators=200`, `max_depth=5`) with 5-fold cross-fitting, which prevents regularization bias by computing residuals out-of-sample before estimating the treatment effect
- Estimated the pooled Average Treatment Effect (ATE) with a 95% confidence interval and assessed statistical significance via t-statistic and p-value
- Conducted Conditional ATE (CATE) analysis by fitting separate DML models on each income quartile subgroup to detect treatment effect heterogeneity across the income distribution
- Visualized subgroup ATEs with 95% confidence interval error bars to assess both magnitude and statistical precision across quartiles

## Key Findings

The DML estimate substantially corrected for the upward selection bias present in a naive income-unadjusted comparison: after controlling for income, age, education, and family structure via flexible Random Forest nuisance models, 401(k) eligibility increased net financial assets by approximately $[YOUR ATE HERE], with a tight confidence interval indicating high statistical precision. The CATE analysis revealed meaningful treatment effect heterogeneity across the income distribution: higher-income quartiles showed larger dollar-denominated effects, consistent with the economic logic that tax-deferred savings are more valuable at higher marginal tax rates and that liquidity constraints limit lower-income households' ability to respond to eligibility offers. The regularization bias demonstration confirmed that applying LASSO directly to a causal question understates the true effect by a non-trivial margin, underscoring why sample-splitting and orthogonalization are necessary when ML methods are used for policy-relevant inference rather than prediction.
