# Lab 5: The Architecture of Bias
### Cassandra Cinzori | Northeastern University

---

## Overview

This lab investigates how data is collected and split before a model ever trains — and why getting that wrong silently poisons everything downstream. Through three progressive phases, we expose **Sampling Error**, eliminate **Covariate Shift**, and forensically detect **Sample Ratio Mismatch (SRM)** in A/B tests.

---

## Tech Stack

- **Python** — pandas, numpy
- **scipy** — Chi-Square hypothesis testing
- **sklearn** — `train_test_split` with stratification
- **Dataset** — Titanic (via seaborn)

---

## Methodology

### Phase 1: The Danger of Randomness (Manual Split)
Manually shuffled the Titanic dataset using `numpy` and performed an 80/20 train/test split without any stratification. Measured the **survival rate delta** between the two sets to demonstrate that Simple Random Sampling (SRS) can produce meaningfully different distributions by chance alone — a **Sampling Error**, not a model error.

### Phase 2: Stratification (The Fix)
Used `sklearn.model_selection.train_test_split` with `stratify=df['pclass']` to force identical passenger class distributions across both sets. This eliminates **Covariate Shift** — the scenario where a key predictor variable (class) is over- or under-represented in one split, causing a model trained on that data to be fundamentally miscalibrated.

### Phase 3: SRM Forensic Audit
Simulated a broken A/B test (450 Control / 550 Treatment out of 1,000 users, planned 50/50) and used `scipy.stats.chisquare` to test whether the imbalance could be explained by chance. A p-value below 0.01 triggers a **CRITICAL FAILURE** flag — indicating an engineering bug (e.g., a misconfigured load balancer), not natural variance.

---

## Key Results

| Check | Value |
|---|---|
| Manual Split Survival Delta | ~0.04–0.08 (varies by seed) |
| Stratified Train Class 1 % | ≈ 24.2% |
| Stratified Test Class 1 % | ≈ 24.2% |
| SRM Chi-Square Statistic | 10.0 |
| SRM P-Value | ~0.0016 → **CRITICAL FAILURE** |

---

## Theoretical Question: Survivorship Bias & the Heckman Correction

### Why does analyzing only Unicorn startups on TechCrunch lead to Survivorship Bias?

TechCrunch and similar outlets overwhelmingly cover **successful** companies — the ones that raised big rounds, went public, or got acquired. The thousands of startups that failed, pivoted quietly, or never gained traction are systematically absent from the data. If you build a model on this dataset to predict "what makes a startup succeed," you're training on a sample that has already been filtered by the outcome you're trying to predict. The result is a model that confidently identifies patterns in winners while having no information about why losers lost.

This is **Survivorship Bias**: the population you *observe* is not the population you *care about*.

### What Ghost Data would fix it with a Heckman Correction?

The **Heckman Selection Model** fixes this by explicitly modeling *why* certain observations made it into your dataset in the first place. To apply it here, you would need:

1. **A "Selection Equation" dataset** — records of *all* startups that existed, not just the ones that got covered. This could come from sources like Crunchbase (including failed companies), SEC filings, or state business registration databases. The goal is to model the probability that a startup *appears in TechCrunch* as a function of observable characteristics (funding stage, sector, founding team size, etc.).

2. **The outcome dataset** — performance metrics (revenue growth, exit valuation) for the startups you *do* observe.

The Heckman model first estimates a **selection probit** (step 1), extracts the **Inverse Mills Ratio** as a correction term, and then includes that term in the main regression (step 2). This statistically accounts for the missing failures — turning ghost data into a bias correction rather than an invisible distortion.

**In short:** the ghost data you need is every startup that *tried and failed to get covered* — the dark matter of the startup ecosystem that TechCrunch never wrote about.

---

## Files
- `the_architecture_of_bias.py` — Full lab implementation
