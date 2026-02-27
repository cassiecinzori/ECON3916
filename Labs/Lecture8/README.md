# Hypothesis Testing & Causal Evidence Architecture

## Objective
Pivoted from pure estimation to formal falsification — operationalizing the scientific method to adjudicate between competing causal narratives in the Lalonde (1986) experimental dataset by subjecting treatment effect claims to rigorous statistical scrutiny under both parametric and non-parametric frameworks.

## Technical Approach
- **Data:** Lalonde (1986) experimental subset — a randomized control trial of the National Supported Work (NSW) job training program, split into `treat = 1` (training recipients) and `treat = 0` (controls) on 1978 real earnings (`re78`).
- **Welch's T-Test (Parametric):** Computed the signal-to-noise ratio of the Average Treatment Effect (ATE) using `scipy.stats.ttest_ind` with `equal_var=False`, accounting for unequal group variances without assuming homoscedasticity.
- **Permutation Test (Non-Parametric):** Validated findings against non-normal, heavy-tailed earnings distributions by running a permutation test across 10,000 resamples via `scipy.stats.permutation_test` — constructing an empirical null distribution that makes zero assumptions about the underlying data-generating process.
- **Type I Error Control:** Pre-committed to α = 0.05 before running any tests, guarding against data dredging and ensuring the rejection of the null hypothesis was governed by protocol rather than post-hoc rationalization.
- **Visualization:** Plotted Kernel Density Estimates (KDE) for both groups to make the distributional "shift" caused by training visible — translating a statistical result into an interpretable economic narrative.

## Key Findings
| Metric | Result |
|---|---|
| Mean Earnings — Treated | ~$6,349 |
| Mean Earnings — Control | ~$4,555 |
| Treatment Effect (ATE) | ~+$1,795 |
| T-Test P-Value | < 0.05 ✓ |
| Permutation P-Value | < 0.05 ✓ |

Both the parametric and non-parametric tests converged on a statistically significant positive treatment effect, rejecting the null hypothesis of no effect via proof by statistical contradiction. Convergence across both methods strengthens confidence that the result is not an artifact of distributional assumptions.

## Business Insight: Hypothesis Testing as the Safety Valve of the Algorithmic Economy
In production data environments — where hundreds of features, segments, and time windows are available for slicing — the temptation to surface "significant" results through exhaustive search is ever-present. Rigorous hypothesis testing is the institutional safeguard against this failure mode. By pre-committing to a falsification framework before observing outcomes, analysts prevent spurious correlations from masquerading as causal signals and protect decision-makers from acting on noise. In an economy increasingly governed by algorithmic recommendations, credit models, and automated pricing, the discipline of formal hypothesis testing is not a methodological formality — it is a mechanism of accountability.

## Concept Extension: Decision Thresholds as Business Parameters
Industry practitioners at firms like Netflix treat statistical significance thresholds not as fixed scientific conventions but as tunable business parameters calibrated to the cost of each error type. Where academic convention defaults to p < 0.05, Netflix's return-aware experimentation framework weights the threshold against the revenue cost of a false positive (shipping a harmful feature) versus a false negative (suppressing a valuable one) — meaning a high-traffic recommendation change may demand p < 0.01 while a low-stakes UI tweak might tolerate p < 0.10. This reflects a broader principle: the α level is an economic decision, not a law of nature. My work in this lab grounds that intuition formally — understanding that when I set a significance threshold, I am making an implicit statement about the relative costs of being wrong in each direction.

## Tools & Stack
`Python` · `SciPy` · `NumPy` · `Pandas` · `Seaborn` · `Matplotlib` · `Welch's T-Test` · `Permutation Testing`

## Data Source
**Dataset:** Lalonde (1986) experimental subset — NSW randomized control trial
**Load directly:**
```python
df = pd.read_csv('lalonde.csv')
```
