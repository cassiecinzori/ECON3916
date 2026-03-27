# The Polynomial Trap: Bias-Variance Tradeoff

## Overview
This project investigates the fundamental tension between model complexity and generalization through two empirical case studies. Using synthetic data generated from y = sin(2πx) with additive Gaussian noise (σ = 0.3), I fit polynomial regressions of degrees 1–15 and constructed complexity curves plotting training versus test RMSE across the full degree range. Results confirmed the classic U-shaped test error curve, with degrees 3–5 minimizing out-of-sample error while higher-degree models exhibited severe overfitting — training RMSE approaching zero as test RMSE climbed sharply.

## Methods
To operationalize model selection without test set leakage, I implemented 5-fold cross-validation manually using NumPy index arithmetic, then validated results against scikit-learn's `cross_val_score`. CV-selected degree matched the true test-optimal degree, demonstrating that cross-validation reliably approximates generalization error in practice.

Applying these principles to the Ames Housing dataset (1,460 observations, 80 features), I compared a kitchen-sink linear model against a parsimonious 5-feature model selected by absolute correlation with sale price. Despite lower training R², the 5-feature model achieved superior CV RMSE — a concrete illustration of how high-dimensional models overfit when the predictor-to-observation ratio is elevated.

## Key Findings
- Polynomial degrees 3–5 were optimal for synthetic sine-wave data (n = 50 train, n = 200 test)
- 5-fold CV-selected degree matched the true test-optimal degree without test set exposure
- On Ames Housing data, a 5-feature model outperformed an 80-feature kitchen-sink model in CV RMSE despite lower training R²

## Tools & Libraries
`Python` · `NumPy` · `scikit-learn` · `Matplotlib`

> *PolynomialFeatures · LinearRegression · make_pipeline · cross_val_score*
