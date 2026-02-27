# Recovering Experimental Truths via Propensity Score Matching

## Objective
Applied Propensity Score Matching (PSM) to an observational dataset to correct for systematic selection bias and recover a credible causal estimate of job training program effectiveness — bridging the gap between observational convenience and experimental rigor.

## Methodology
- **Diagnosed Observational Failure:** Identified severe selection bias in the PSID control group, whose members were systematically older, wealthier, and more stably employed than NSW program trainees, invalidating naive group comparisons.
- **Modeled Selection into Treatment:** Estimated propensity scores — the conditional probability of treatment assignment given observed covariates — using a logistic regression model with the standard Lalonde specification (age, education, race, marital status, degree attainment, and pre-treatment earnings in 1974 and 1975).
- **Implemented Nearest Neighbor Matching:** Constructed a matched comparison group by pairing each treated unit with its closest control analog in propensity score space via 1:1 nearest-neighbor matching with replacement, minimizing bias from the limited control pool.
- **Validated Covariate Balance:** Confirmed successful matching by verifying that Standardized Mean Differences (SMD) across all covariates fell below the 0.1 threshold, satisfying the assumption of approximate ignorability in the matched sample.
- **Estimated the Causal Effect:** Applied an independent samples t-test to the matched dataset to produce an unconfounded estimate of average treatment effect on the treated (ATT).

## Key Findings
| Estimator | Earnings Effect |
|---|---|
| Naïve Difference-in-Means (Unmatched) | −$15,204 |
| PSM-Adjusted Estimate (Matched) | +$1,800 |

The naïve comparison — corrupted by selection bias — suggested job training *reduced* annual earnings by over $15,000, an economically implausible result that perfectly illustrates the dangers of uncontrolled observational inference. After matching on propensity scores and achieving balance across all pre-treatment covariates, the recovered estimate of **+$1,800** aligns closely with the experimental benchmark established by the original randomized NSW trial, confirming that PSM successfully isolated the true causal effect of training on 1978 earnings.

## Data Source
**Dataset:** Lalonde (1986) observational subset — NSW treated units paired with PSID comparison group controls.
**Repository:** [`robjellis/lalonde`](https://github.com/robjellis/lalonde/blob/master/lalonde_data.csv) — `lalonde_data.csv`
**Load directly in Python:**
```python
url = "https://raw.githubusercontent.com/robjellis/lalonde/master/lalonde_data.csv"
df = pd.read_csv(url)
```

## Tools & Stack
`Python` · `Pandas` · `Scikit-Learn` · `SciPy` · `Logistic Regression` · `Nearest Neighbor Matching`
