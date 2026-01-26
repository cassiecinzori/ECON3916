# Lab 3: Vietnam Economic Dashboard - The Comparative Mindset

## Overview
This lab demonstrates how trends without context can be misleading. We analyze Vietnam's economy by fetching data from the World Bank API, visualizing individual indicators, and ultimately synthesizing them into an executive dashboard.

**Key Learning:** A line going "up" can look impressive in isolation, but benchmarking against global averages reveals the full story.

---

## Lab Structure

### Phase 1: Foundations First (NO AI ALLOWED)
**Objective:** Manually fetch, clean, and calculate economic indicators to build foundational understanding.

#### Step 1: Setup
Install the World Bank API library and define indicator mappings:
```python
!pip install wbgapi
import wbgapi as wb
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

country_codes = ['VNM', 'UMC', 'WLD']  # Vietnam, Upper Middle Income, World
```

We track 12 economic indicators covering:
- **Wealth:** GDP Per Capita, Total GDP
- **Labor:** Participation Rate, Unemployment, Labor Force
- **Inflation:** CPI-based inflation
- **Savings/Investment:** Gross Domestic Savings, Capital Formation
- **Trade:** Exports, Imports
- **Fiscal:** Tax Revenue, Government Expenditure

#### Step 2: Data Ingestion & Cleaning
Fetch data from World Bank API (2000-2025), transpose the DataFrame, clean the index, and extract Vietnam-specific data:
```python
df_raw = wb.data.DataFrame(indicators, economy=country_codes, time=range(2000, 2025))
df = df_raw.T
df.index = df.index.str.replace('YR', '').astype(int)
df_vnm = df.xs('VNM', axis=1, level=0).copy()
```

#### Step 3: Calculate Derived Metrics
Manually compute four key indicators:
1. **Natural Rate of Unemployment:** 5-year moving average of unemployment
2. **Productivity:** GDP per worker (GDP ÷ Labor Force)
3. **Net Capital Outflow (NCO):** Exports - Imports
4. **Budget Balance:** Tax Revenue - Government Spending

---

### Phase 2: The Story of Visualization (Manual Practice)

You must hand-code 8 exercises to understand how visualization choices shape narratives:

#### Exercise 1: The "Narrow View"
Plot Vietnam's GDP Per Capita alone. Notice how impressive the growth looks without context.

#### Exercise 2: The "Full Picture"
Add Upper Middle Income and World averages as benchmarks. The story reveals Vietnam's remarkable convergence trajectory—starting well below both benchmarks in 2000 but rapidly closing the gap through export-led industrialization.

#### Exercise 3-8: Component Visualizations
Build individual charts for:
- **Wealth & Growth:** Total GDP vs GDP Per Capita (side-by-side subplots)
- **Labor Market:** Participation Rate and Unemployment (stacked vertically)
- **Inflation:** Bar chart showing annual inflation rates
- **Savings & Investment:** Line plot comparing domestic savings vs capital formation
- **Trade Balance:** Fill-between visualization of Exports vs Imports with NCO line
- **Fiscal Policy:** Structural gap between Tax Revenue and Government Expenditure

**Key Insight:** Each exercise reinforces how different chart types and benchmarks tell different stories.

---

### Phase 4: AI Dashboard Synthesis (AI AUTHORIZED & REQUIRED)

**Objective:** Act as a Lead Data Scientist. Use AI to synthesize all 6 economic areas into a single 2×3 Executive Dashboard.

#### Why Use AI Here?
You've manually built the components and understand the underlying data. Now you leverage AI to accelerate the synthesis—exactly how professionals work.

#### The Prompt
Paste this into Claude (or your preferred AI):
```
I have a DataFrame 'df_vnm' containing economic indicators for Vietnam.
I need to create a **2x3 Executive Dashboard** summarizing the economy using Matplotlib/Seaborn.

**The Variables:**
* Real GDP: 'GDP_Const'
* Inflation: 'Inflation_CPI'
* Unemployment: 'Unemployment_Rate'
* Tax Revenue: 'Tax_Rev_GDP'
* Gov Expenditure: 'Gov_Exp_GDP'
* Exports: 'Exports_GDP'
* Imports: 'Imports_GDP'
* Savings: 'Gross_Dom_Savings'
* Investment: 'Gross_Cap_Formation'

**Requirements:**
1. Top Left: Real GDP (Line chart)
2. Top Middle: Inflation Rate (Bar chart with horizontal line at 0)
3. Top Right: Unemployment Rate (Line chart)
4. Bottom Left: Fiscal Balance (Fill area between Tax Revenue and Gov Expenditure)
5. Bottom Middle: Trade Balance (Fill area between Exports and Imports)
6. Bottom Right: Savings vs Investment (Dual lines)

**Style:**
* Use plt.style.use('dark_background')
* Add main title: 'Vietnam Economic Snapshot'
* Use tight_layout() to prevent overlap
```

#### What AI Provides
The AI generates complete production-ready code that:
- Creates a 2×3 grid layout synthesizing all 6 economic areas
- Uses consistent styling (dark background, proper spacing)
- Implements appropriate chart types for each metric
- Labels and formats everything professionally

#### The 6 Economic Areas Synthesized
1. **Wealth:** Real GDP trajectory
2. **Labor:** Unemployment trends
3. **Inflation:** Price stability via CPI
4. **Fiscal:** Government balance (revenue vs expenditure with surplus/deficit shading)
5. **Trade:** External balance (exports vs imports with surplus/deficit shading)
6. **Savings:** Domestic savings vs capital formation

---

## Key Takeaways

1. **Context is everything:** Vietnam's GDP growth looks impressive alone, but benchmarking reveals a dramatic convergence story—rapidly catching up to Upper Middle Income peers
2. **Visualization choices matter:** Chart types, axes, and comparisons fundamentally alter the narrative
3. **AI as a productivity tool:** After understanding components manually, AI accelerates synthesis and production
4. **The comparative mindset:** Always ask "compared to what?" when evaluating economic performance

---

## Files in This Repository
- `lab3_vietnam_analysis.ipynb` - Main analysis notebook with all exercises
- `README.md` - This file
- `requirements.txt` - Python dependencies (wbgapi, pandas, matplotlib, seaborn)

## Running the Lab
```bash
pip install -r requirements.txt
jupyter notebook lab3_vietnam_analysis.ipynb
```
