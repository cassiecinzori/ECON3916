# Causality & Spurious Regression in Macroeconomic Time-Series Data

## Overview

This project demonstrates a core challenge in applied econometrics: the tendency for macroeconomic variables to appear highly correlated simply because they share a common upward trend over time — not because one structurally causes the other. Using live data from the Federal Reserve Economic Data (FRED) API, this analysis walks through a full diagnostic pipeline, from identifying the correlation trap to resolving it through principled data transformation and causal reasoning.

---

## Objectives

- Expose spurious correlations that emerge in raw, non-stationary macroeconomic levels data
- Quantify multicollinearity using Variance Inflation Factor (VIF) diagnostics
- Eliminate trend-driven correlation artifacts via Year-over-Year (YoY) growth rate transformation
- Map true structural relationships using Directed Acyclic Graphs (DAGs)

---

## Dataset

Five macroeconomic indicators were pulled directly from FRED via `pandas_datareader`, spanning January 2010 – January 2024:

| FRED Series | Variable | Description |
|-------------|----------|-------------|
| `CPIAUCSL` | CPI | Consumer Price Index |
| `UNRATE` | Unemployment Rate | Civilian unemployment (%) |
| `FEDFUNDS` | Fed Funds Rate | Federal Reserve policy rate |
| `INDPRO` | Industrial Production | Index of industrial output |
| `M2SL` | M2 Money Supply | Broad money supply |

---

## Methodology

### 1. Correlation Trap Visualization
Raw level data was plotted as a Pearson correlation heatmap using `seaborn`. Variables like CPI and M2 exhibited correlations approaching **r = 0.99** — a textbook example of spurious regression driven by shared time trends rather than structural causation.

### 2. Multicollinearity Diagnostics (VIF)
Variance Inflation Factors were computed via `statsmodels` for all predictors in a regression framework targeting CPI. VIF scores well above the conventional threshold of 10 confirmed severe multicollinearity in the raw data, indicating that regression coefficients derived from these untransformed variables would be statistically unreliable.

### 3. YoY Growth Rate Transformation
Trending variables (CPI, Industrial Production, M2) were converted to Year-over-Year percentage growth rates using the formula:

$$\text{YoY}_t = 100 \times \left(\frac{X_t}{X_{t-12}} - 1\right)$$

This transformation removes the non-stationary trend component, shifting the focus from absolute levels to short-run structural dynamics. The resulting correlation heatmap showed a substantial reduction in inter-variable correlations, particularly between CPI and M2.

### 4. Interactive Dashboard (Plotly)
An interactive Plotly heatmap dashboard was built with a dropdown menu allowing direct comparison between the raw levels and YoY-transformed correlation matrices. A fixed color scale (`zmin=-1, zmax=1`) ensures visual comparability across both views.

### 5. Causal Graphing (DAG)
A Directed Acyclic Graph was constructed using `networkx` to encode causal assumptions prior to any regression modeling. The DAG identified **Expansionary Macro Policy** as an unobserved common cause (fork) of both M2 and CPI — explaining why their raw correlation far exceeds what the direct M2 → CPI path (quantity theory of money) alone would produce. Additional structural relationships encoded include Okun's Law and the Taylor Rule feedback loop.

---

## Key Findings

- Raw CPI–M2 correlation (~0.99) is largely **spurious**, driven by a shared time trend rather than direct causation
- VIF scores confirmed **severe multicollinearity** across trending predictors in levels form
- YoY transformation meaningfully reduced inter-variable correlations, isolating short-run structural signals
- DAG analysis revealed that the CPI–M2 relationship is best understood as a **fork** (common cause) plus a direct causal path — a distinction that raw correlation alone cannot reveal

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| `pandas` | Data ingestion, resampling, transformation |
| `pandas_datareader` | Live FRED API data retrieval |
| `seaborn` / `matplotlib` | Static correlation heatmaps |
| `statsmodels` | VIF diagnostics, regression framework |
| `plotly` | Interactive heatmap dashboard |
| `networkx` | DAG construction and visualization |

---

## Skills Demonstrated

- Time-series data wrangling and stationarity correction
- Multicollinearity diagnosis and remediation
- Causal inference fundamentals (DAGs, confounders, fork structures)
- Interactive data visualization for analytical storytelling
- Applied macroeconomic reasoning (Quantity Theory, Okun's Law, Taylor Rule)
