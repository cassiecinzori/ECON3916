# Audit 02: Deconstructing Statistical Lies

## Executive Summary
As Data Quality Auditor at Pareto Ventures, I conducted forensic analysis on three portfolio companies claiming "perfect" metrics. This audit reveals how averages conceal critical operational risks through three case studies in robustness, probability, and survivorship bias.

## Key Findings

### 1. NebulaCloud: The Latency Trap
**Claim:** Mean latency of 35ms demonstrates stable server performance  
**Reality:** Tail latency reveals 2% of requests experience 1000-5000ms spikes

**Statistical Evidence:**
- Standard Deviation: 318ms (inflated by outliers)
- Median Absolute Deviation: 11ms (robust measure)
- **Verdict:** Mean is a vanity metric. SD/MAD ratio of 29x proves extreme outlier sensitivity.

**Business Impact:** While 98% of users experience 20-50ms latency, the "average" user doesn't exist. Enterprise SLAs require P99 metrics, not means.

### 2. IntegrityAI: The False Positive Paradox
**Claim:** 98% accurate plagiarism detection (Sensitivity=98%, Specificity=98%)  
**Reality:** In low-prevalence environments, precision collapses

**Bayesian Analysis:**
| Context | Base Rate | P(Cheater\|Flagged) | False Positive Rate |
|---------|-----------|-------------------|---------------------|
| Bootcamp | 50% | 98.00% | 2.00% |
| Econ Class | 5% | 71.68% | 28.32% |
| Honors Seminar | 0.1% | 4.67% | **95.33%** |

**Verdict:** When cheating is rare (0.1%), flagging a student means 95% chance they're innocent. Marketing accuracy ≠ operational precision.

### 3. FinFlash: Sample Ratio Mismatch
**Claim:** A/B test with 50/50 split shows treatment wins  
**Reality:** 500 missing users in treatment group (χ² = 2.5)

**Chi-Square Test:**
- Observed: Control=50,250 | Treatment=49,750
- Expected: 50,000 | 50,000
- **Verdict:** χ² = 2.5 < 3.84 (not significant at p<0.05), but warrants investigation

**Recommendation:** While not statistically invalid, the 500-user discrepancy suggests potential app crashes or pipeline bias requiring engineering review.

### 4. Pump.fun: The Memecoin Graveyard
**Claim:** Analysis of successful tokens shows strong ROI potential  
**Reality:** 99% of tokens failed and were excluded from analysis

**Survivorship Bias Simulation (n=10,000 tokens):**
- Mean Market Cap (All tokens): $12,458
- Mean Market Cap (Top 1% only): $156,234
- **Bias Factor:** 12.5x inflation

**Verdict:** Platforms that delist failures create statistical mirages. Analyzing only "Listed Coins" guarantees 98.6% of the data generating process is invisible.

## Methodological Approach

**Phase 1-3:** Manual implementation of MAD, Bayes' Theorem, and Chi-Square tests to prove algorithmic literacy  
**Phase 4:** AI-assisted expansion using P.R.I.M.E. framework for complex simulations

## Technical Skills Demonstrated
- Robust statistics (MAD vs SD for outlier detection)
- Bayesian inference (base rate fallacy in classification)
- Hypothesis testing (SRM detection via χ² goodness of fit)
- Monte Carlo simulation (power law distributions)
- Data visualization (dual histograms exposing survivorship bias)

## Strategic Recommendations
1. **Replace vanity metrics:** Use P95/P99 latency instead of means
2. **Contextualize accuracy:** Require precision/recall for low-prevalence scenarios
3. **Monitor randomization:** Automated SRM detection in A/B platforms
4. **Demand complete data:** Access to "graveyard" datasets, not just survivors

---
*Cassie | Data Quality Auditor | Pareto Ventures*
