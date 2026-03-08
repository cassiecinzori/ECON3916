# ECON3916 Assignment 3 — Statistical & Causal Inference Methods
**Cassandra Cinzori** | Northeastern University

---

## Overview
This notebook applies three core econometric and statistical methods to real-world-style datasets: bootstrapping for non-parametric inference, permutation testing for A/B experiment falsification, and propensity score matching for causal effect estimation.

---

## Structure

### Phase 1 — Bootstrapping Non-Parametric Uncertainty
Simulates a zero-inflated gig economy tip distribution (100 zero-tip rides + 150 exponential draws) and constructs a 95% confidence interval for the median via 10,000 manual bootstrap resamples. Demonstrates why parametric normal CIs are inappropriate for skewed, bounded distributions.

**Output:** `phase1_bootstrap.png`

### Phase 2 — Falsification in Logistics A/B Testing
Generates synthetic delivery time data (control: Normal, treatment: Log-Normal) and tests for a statistically significant difference using a 5,000-iteration permutation test. Computes an empirical two-sided p-value without distributional assumptions.

**Output:** `phase2_permutation.png`

### Phase 3 — Causal Control via Propensity Score Matching
Loads `swiftcart_loyalty.csv` and estimates the causal effect of a loyalty subscription program on post-treatment spending. Compares the naive Simple Difference in Outcomes (SDO) against the Average Treatment Effect on the Treated (ATT) after 1:1 nearest-neighbor propensity score matching using logistic regression.

### Phase 4 — Love Plot: Covariate Balance Diagnostics
Visualizes Standardized Mean Differences (SMDs) for all pre-treatment covariates before and after PSM, confirming successful bias reduction when all post-match SMDs fall within the |SMD| < 0.1 threshold.

**Output:** `phase4_love_plot.png`

---

## Requirements
```
pandas numpy matplotlib seaborn scikit-learn
```

## Data
| File | Description |
|------|-------------|
| `swiftcart_loyalty.csv` | SwiftCart user data with columns: `subscriber`, `pre_spend`, `account_age`, `support_tickets`, `post_spend` |

---

## Key Results
| Method | Estimate |
|--------|----------|
| Bootstrap 95% CI (Median tip) | Asymmetric — lower bound near $0 |
| Permutation p-value | See console output |
| Naive SDO | Upward-biased due to selection |
| Causal ATT (PSM) | Corrected estimate after matching |
