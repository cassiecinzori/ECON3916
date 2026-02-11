# The Engine of Inference

**Author:** Cassandra Cinzori  
**Topic:** Inferential Statistics & Monte Carlo Simulation

## Overview

This project demonstrates the transition from descriptive to inferential statistics through computational simulation. Using real-world applications in sports betting, cryptocurrency, venture capital, and startup finance, we explore fundamental statistical concepts that power modern data-driven decision making.

## Modules

### Module A: The Law of Large Numbers (Sports Betting)
**Objective:** Visualize why "the house always wins" and quantify sampling error

- **Key Concept:** -110 odds require a 52.38% win rate to break even
- **Simulation:** 5,000 bets showing convergence below profitability threshold
- **Insight:** Average bettors (50% win rate) are guaranteed to lose money over time

### Module B: The Central Limit Theorem (Crypto Returns)
**Objective:** Prove CLT works even in "fat-tailed" environments

- **Population:** Log-normal distribution mimicking Bitcoin returns (skewed, heavy tails)
- **Simulation:** Sample sizes n=1, 2, 30 showing distribution of means becoming normal
- **Insight:** Even chaotic markets follow predictable patterns at scale

### Module C: Confidence Intervals (Venture Capital)
**Objective:** Calculate confidence intervals for SaaS metrics (LTV/CAC ratio)

- **The Soup Analogy:** Population size doesn't matter—only sample size does
- **VC Audit:** Compare stable vs. volatile startups using 95% confidence intervals
- **Decision Rule:** Invest only if lower bound > 3.0 benchmark

### Module D: Correlated Simulation (Startup Runway)
**Objective:** Model realistic startup finances with correlated revenue/costs

- **Naive Model:** Independent revenue and burn (unrealistic)
- **Correlated Model:** Revenue-burn correlation (ρ=0.7) acts as natural hedge
- **Result:** Correlated model shows ~50% lower bankruptcy risk

## Technical Stack

```python
numpy          # Monte Carlo simulations
matplotlib     # Visualization
seaborn        # Statistical plotting
```

## Key Learning Outcomes

1. **Law of Large Numbers:** Understanding convergence and expected value
2. **Sampling Error:** Quantifying uncertainty in estimates
3. **Central Limit Theorem:** Why sample means are normally distributed
4. **Confidence Intervals:** Setting bounds on unknown parameters
5. **Correlation Effects:** How variable relationships impact risk modeling

## Running the Code

### Google Colab (Recommended)
1. Upload `estimation.py` to Google Colab
2. Run all cells sequentially
3. Visualizations will render inline

### Local Jupyter
```bash
pip install numpy matplotlib seaborn
jupyter notebook estimation.ipynb
```

## Results Summary

| Model | Metric | Result |
|-------|--------|--------|
| Sports Betting | Win Rate @ 5000 bets | ~50% (below 52.38% breakeven) |
| Crypto CLT | Distribution Shape | Normal at n=30 |
| VC Audit (Stable) | 95% CI | [3.9, 4.1] → INVEST |
| VC Audit (Volatile) | 95% CI | [-2.7, 10.7] → PASS |
| Startup (Independent) | Bankruptcy Risk | ~12-18% |
| Startup (Correlated) | Bankruptcy Risk | ~5-8% |

## Philosophy

> "If you can't derive it, simulate it." — Modern Computational Economics

This project embraces Monte Carlo methods as a practical approach to statistical inference, making abstract concepts concrete through code.

## Files

- `estimation.py` - Complete Python implementation
- `estimation.ipynb` - Jupyter notebook version
- `README.md` - This file

---

**Note:** Results will vary slightly due to random simulation—this is expected and demonstrates sampling variability!
