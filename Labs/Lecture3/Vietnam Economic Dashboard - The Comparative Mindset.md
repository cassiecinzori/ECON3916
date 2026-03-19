# Vietnam Economic Snapshot — Executive Dashboard

## Overview
A 2×3 Matplotlib dashboard summarizing Vietnam's key macroeconomic indicators from World Bank data (`df_vnm`). Uses a dark background style for presentation-ready output.

---

## Prerequisites

```python
import matplotlib.pyplot as plt
import seaborn as sns
```

`df_vnm` must be a pandas DataFrame indexed by `Year` (int) with the following columns:

| Column | Description | Unit |
|---|---|---|
| `GDP_Const` | Real GDP at constant prices | Billions USD |
| `Inflation_CPI` | CPI-based inflation rate | % |
| `Unemployment_Rate` | Unemployment rate | % |
| `Tax_Rev_GDP` | Tax revenue | % of GDP |
| `Gov_Exp_GDP` | Government expenditure | % of GDP |
| `Exports_GDP` | Exports | % of GDP |
| `Imports_GDP` | Imports | % of GDP |
| `Gross_Dom_Savings` | Gross domestic savings | % of GDP |
| `Gross_Cap_Formation` | Gross capital formation (investment) | % of GDP |

---

## Dashboard Layout

```
┌─────────────────┬─────────────────┬─────────────────┐
│   Real GDP      │  Inflation Rate │  Unemployment   │
│   (Line)        │  (Bar + h-line) │  (Line)         │
├─────────────────┼─────────────────┼─────────────────┤
│  Fiscal Balance │  Trade Balance  │  Savings vs     │
│  (Fill between) │  (Fill between) │  Investment     │
└─────────────────┴─────────────────┴─────────────────┘
```

### Panel Descriptions

**Top Left — Real GDP**
Line chart of `GDP_Const`. Tracks the absolute size of Vietnam's economy over time.

**Top Middle — Inflation Rate**
Bar chart of `Inflation_CPI` with a dashed horizontal line at y=0 to distinguish positive/negative inflation years.

**Top Right — Unemployment Rate**
Line chart of `Unemployment_Rate`. Reflects labor market conditions.

**Bottom Left — Fiscal Balance**
Dual lines for `Tax_Rev_GDP` and `Gov_Exp_GDP` with filled area between them. Green fill = surplus (revenue > expenditure); red fill = deficit.

**Bottom Middle — Trade Balance**
Dual lines for `Exports_GDP` and `Imports_GDP` with filled area between them. Green fill = trade surplus; red fill = trade deficit.

**Bottom Right — Savings vs Investment**
Dual lines for `Gross_Dom_Savings` and `Gross_Cap_Formation`. Gaps between lines indicate net capital inflow/outflow.

---

## Style Notes
- `plt.style.use('dark_background')` applied globally before figure creation
- Main title: `'Vietnam Economic Snapshot'` via `fig.suptitle()`
- Grid lines at `alpha=0.3` on all panels for readability without visual clutter
- `plt.tight_layout()` called before `plt.show()` to prevent title/label overlap

---

## Usage

```python
plt.style.use('dark_background')
fig, axes = plt.subplots(2, 3, figsize=(18, 10))
fig.suptitle('Vietnam Economic Snapshot', fontsize=20, fontweight='bold', y=0.98)

# ... panel code ...

plt.tight_layout()
plt.show()
```
