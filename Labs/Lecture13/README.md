# The Architecture of Dimensionality: Hedonic Pricing & the FWL Theorem

## Objective
Estimated a multivariate hedonic pricing model on 2026 California real estate data to manually execute the Frisch-Waugh-Lovell theorem, proving algebraically how OLS isolates pure partial effects by partialling out confounding variance.

## Data
Zillow synthetic dataset — 2026 California residential market. Features: `Home_Value`, `Property_Age`, `Distance_to_Transit`.

## Tech Stack
Python 3.10+ · pandas · statsmodels.formula.api · matplotlib · plotly

## Methodology
- **Baseline bivariate regression** — modeled `Home_Value ~ Property_Age` in isolation to expose the distortion introduced by omitting a correlated confounder
- **Multivariate expansion** — added `Distance_to_Transit` to absorb location variance, recovering the true partial coefficient on age
- **FWL manual execution (3-step residual extraction):**
  - Regressed `Home_Value` on `Distance_to_Transit`; extracted price residuals
  - Regressed `Property_Age` on `Distance_to_Transit`; extracted age residuals
  - Regressed price residuals on age residuals (no intercept) to recover the isolated partial slope
- **Epistemological proof** — confirmed exact decimal-place equivalence between the FWL residual coefficient and the multivariate OLS coefficient

## Key Findings
The naive bivariate model exhibited severe omitted variable bias: because older homes cluster near high-value transit corridors, omitting distance caused the algorithm to misattribute location premium to physical age. The resulting coefficient was directionally misleading. Introducing `Distance_to_Transit` as a control variable corrected this misallocation. Manual execution of the FWL theorem confirmed that OLS implicitly performs residual partialling — the coefficient recovered through sequential residual regression matched the multivariate result exactly, demonstrating that algorithmic ceteris paribus is not an assumption but a mathematical guarantee of the OLS projection.
