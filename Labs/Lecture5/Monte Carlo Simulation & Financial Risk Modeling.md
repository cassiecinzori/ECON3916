# Monte Carlo Simulation & Financial Risk Modeling

**Author:** Cassandra Cinzori  
**Course:** ECON 3916 - Statistical & Machine Learning for Economics  
**Date:** February 2025

## Overview

This project uses Monte Carlo simulation to quantify financial risk and determine capital reserve requirements for a SaaS business with $10M base revenue. By running 10,000+ probabilistic scenarios, we calculate Value at Risk (VaR) and demonstrate how distributional assumptions critically impact risk assessment.

## Business Problem

A SaaS company faces revenue uncertainty from two sources:
- **Customer Churn:** Existing customers canceling (μ=10%, σ=2%)
- **New Sales:** Variable customer acquisition (μ=$1.5M, σ=$500K)

**Question:** How much capital should the company hold in reserve to survive extreme downside scenarios?

## Methodology

### Revenue Model
```
Net Revenue = Base Revenue × (1 - Churn Rate) + New Sales
```

### Simulation Process
1. Generate 10,000 random scenarios for churn and sales
2. Calculate resulting revenue distribution
3. Compute risk metrics:
   - **Probability of Revenue Decline:** Likelihood of ending below $10M
   - **95% Value at Risk (VaR):** Worst-case at 95% confidence
   - **Capital Reserve:** Buffer needed to cover downside

## Key Findings

### Normal Distribution Model (Standard Assumption)
- 95% VaR: ~$9.61M
- Probability of Decline: 17.65%
- **Required Capital Reserve: ~$390K**

### Fat Tail Model (Student's t-distribution, df=3)
- 95% VaR: ~$9.31M  
- Probability of Decline: 20.20%
- **Required Capital Reserve: ~$689K**

### Critical Insight
**Normal distribution assumptions underestimate required reserves by ~$300K.**

Real-world business volatility exhibits "fat tails"—rare but severe outcomes occur more frequently than the bell curve predicts. Companies using normal distribution assumptions are undercapitalized for market crashes, competitive disruptions, or macroeconomic shocks.

## Why This Matters

**For Financial Institutions:**
- Portfolio VaR calculations
- Regulatory capital requirements (Basel III)
- Stress testing and scenario analysis

**For Corporate Finance:**
- Working capital planning
- Cash flow forecasting under uncertainty
- Risk-adjusted decision making

**The Bottom Line:** The cost of holding additional reserves is far less than the existential risk of insolvency during extreme market conditions.

## Technical Implementation

**Core Functions:**
- `simulate_law_of_large_numbers()` - Demonstrates probability convergence
- `monty_hall_sim()` - Validates counterintuitive probability
- `saas_risk_model()` - Models revenue under Normal distribution
- `fat_tail_stress_test()` - Compares Normal vs Student's t distributions

**Libraries:** NumPy (simulation), Matplotlib (visualization)

## Results Summary

| Metric | Normal | Fat Tail | Difference |
|--------|--------|----------|------------|
| 95% VaR | $9.61M | $9.31M | $300K |
| P(Decline) | 17.65% | 20.20% | +2.55% |
| Capital Reserve | $390K | $689K | +$299K |

## Recommendation

Increase capital reserves by $300K-$800K above normal distribution estimates to protect against Black Swan events. Distribution assumptions aren't just academic—they determine whether a company survives extreme volatility.

## Running the Code
```bash
pip install numpy matplotlib
jupyter notebook monte_carlo_simulation.ipynb
```

## Files
- `monte_carlo_simulation.ipynb` - Main analysis notebook
- `README.md` - This file

---

*Built with Python, NumPy, and Matplotlib | Northeastern University*
