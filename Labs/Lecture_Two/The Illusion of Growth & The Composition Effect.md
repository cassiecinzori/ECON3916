# Lab 2: The Illusion of Growth & The Composition Effect

## Objective

Built a Python pipeline to ingest live economic data from the Federal Reserve Economic Data (FRED) API to analyze long-run wage stagnation and correct for composition bias in labor market statistics. This project demonstrates the critical difference between nominal and real economic indicators, and exposes how workforce composition changes can create misleading signals in aggregate wage data.

## Methodology

### Data Acquisition & Transformation
- **API Integration**: Leveraged the `fredapi` Python library to programmatically fetch real-time macroeconomic data from the St. Louis Federal Reserve database
- **Primary Series**: 
  - `AHETPI` - Average Hourly Earnings of Production & Nonsupervisory Employees
  - `CPIAUCSL` - Consumer Price Index for All Urban Consumers
  - `ECIWAG` - Employment Cost Index for Wages & Salaries
- **Inflation Adjustment**: Converted nominal wages to real (constant-dollar) terms by deflating using CPI, rebased to current dollars to enable historical comparison

### Statistical Bias Detection & Correction
1. **Initial Analysis**: Calculated and visualized real wages from 1964-present, revealing decades of stagnant purchasing power despite rising nominal wages (the "Money Illusion")
2. **Anomaly Detection**: Identified a sharp 2020 spike in average wages that contradicted labor market fundamentals during the pandemic recession
3. **Composition Effect Analysis**: Fetched the Employment Cost Index (ECI)—a fixed-weight index that holds workforce composition constant—to isolate the compositional bias
4. **Comparative Visualization**: Rebased both standard wages and ECI to index form (2015=100) to quantify the divergence and validate the artificial nature of the 2020 spike

### Technical Implementation
- **Tech Stack**: Python, pandas (data manipulation), matplotlib (visualization), fredapi (data ingestion)
- **Data Pipeline**: Automated ETL process from FRED API → DataFrame transformation → statistical adjustment → publication-ready visualizations

## Key Findings: The Pandemic Paradox

### The Money Illusion (1964-Present)
Real wages have remained essentially flat for over 50 years when adjusted for inflation, despite nominal wages increasing nearly 10x. This demonstrates the critical importance of distinguishing between nominal growth (which creates an "illusion" of prosperity) and real purchasing power.

### The 2020 Composition Effect
The pandemic created a statistical artifact in wage data:
- **Standard wage measures** showed a sharp spike in 2020, suggesting workers were suddenly earning more
- **Reality**: Low-wage service workers (retail, hospitality) disproportionately lost jobs, mechanically raising the *average* wage of remaining workers
- **ECI validation**: The composition-adjusted ECI showed stable, modest growth through 2020—confirming the spike was purely compositional, not an actual increase in labor demand or worker bargaining power

This finding illustrates a fundamental econometric principle: **sample selection bias** can make aggregate statistics highly misleading during periods of non-random workforce changes. The analysis demonstrates the importance of using composition-adjusted indices (like ECI) rather than naive averages when analyzing labor market dynamics.

### Policy Implications
The composition effect has real consequences—policymakers relying on standard wage data in 2020 might have incorrectly concluded that workers didn't need additional support, when in reality the opposite was true: the lowest-paid workers bore the brunt of job losses while appearing "invisible" in aggregate wage statistics.

---

**Skills Demonstrated**: API integration, time-series analysis, inflation adjustment, statistical bias detection, econometric reasoning, data visualization for economic storytelling
