**Title:** The Cost of Living Crisis: A Data-Driven Analysis

**Structure:**
1. The Problem: Why the "Average" CPI fails students
2. Methodology: Python, APIs, and Index Theory (mention Laspeyres)
3. Key Findings
4. Visualizations
5. Impact & Implications
6. Technical Skills Demonstrated

---

**MY DATA:**

**Date Range:** January 2016 to January 2026

**Key Findings:**
- National CPI increased 37.2% from 2016-2026
- Student SPI increased 36.9% from 2016-2026
- Current divergence: Student costs are 0.3% LOWER than official CPI (converged in recent years)
- Boston regional premium: 1.9% BELOW national average (unexpected finding)
- Historical pattern: Student costs significantly outpaced CPI from 2016-2020 (visible in Chart 2's 
  shaded "Student Inflation Premium" area), but have since converged
- The 2020-2021 period shows dramatic CPI acceleration that caught up to student-specific costs

**Methodology:**
- **Data Source:** Federal Reserve Economic Data (FRED) API
- **Series Used:** 
  * CPIAUCSL (National CPI)
  * CUSR0000SEEB (Tuition & Fees)
  * CUSR0000SEHA (Rent of Primary Residence)
  * CUSR0000SEFV (Food Away From Home)
  * CUSR0000SERA02 (Cable & Streaming)
  * CUURA103SA0 (Boston-Cambridge-Newton MSA CPI)
- **Normalization:** All indices rebased to January 2016 = 100 using Laspeyres index methodology
- **Custom Index Construction:** Created weighted Student Price Index (SPI) using:
  * Tuition: 40% (vs. ~5% in official CPI)
  * Rent: 30% (vs. ~34% housing in official CPI)
  * Groceries/Necessities: 15%
  * Streaming: 10%
  * Food Away From Home: 5%
- **Key Innovation:** Demonstrated the "Scale Fallacy" - why comparing raw FRED indices with 
  different base years (1982-1984 vs. 1997) produces misleading results

**Charts Created:**

**Chart 1: The Scale Fallacy (2016-2026)**
- Shows RAW, non-normalized data: Tuition (~700-900), Streaming (~430-600), CPI (~237-325)
- Visually demonstrates why different base years make direct comparison statistically invalid
- Includes warning banner: "MISLEADING CHART - DO NOT USE FOR ANALYSIS"
- Teaching moment: Tuition appears 1.5x higher than Streaming, but they measure different time periods

**Chart 2: The Student Inflation Gap (2016-2026)**
- Two normalized lines: Official CPI (blue) and Student SPI (red), both base 2016 = 100
- Shaded "Student Inflation Premium" area between lines (visible 2016-2021)
- Shows convergence: Gap of -0.3 points by 2026 (Student SPI slightly lower than CPI)
- Key insight: Student costs led inflation pre-pandemic, but general inflation caught up post-2020

**Chart 3: Three-Way Comparison (2016-2026)**
- National CPI (grey), Boston CPI (blue), Student SPI (red)
- All normalized to 2016 = 100
- Reveals: Boston costs track closely with national average (slight discount by 2026)
- Shows Student SPI and Boston CPI converge with national trends in recent years
- Challenges assumption that Boston is significantly more expensive (relative to student spending patterns)

**Unexpected Finding:**
Unlike typical cost-of-living analyses that show persistent divergence, this study reveals that 
post-pandemic inflation (2020-2023) disproportionately affected general consumer goods, causing 
the official CPI to catch up with student-specific costs. This suggests:
1. Pandemic-era supply chain disruptions hit broad consumer goods harder than education/rent
2. Student cost structures (weighted toward education) were already elevated pre-pandemic
3. Recent moderation in tuition growth rates (visible in Chart 1's flattening post-2020)

**Technical Skills:**
- Python (pandas, matplotlib, fredapi)
- API integration and automated data retrieval
- Statistical normalization and index construction (Laspeyres methodology)
- Weighted composite index design
- Data visualization and narrative storytelling
- Economic theory application (price indices, regional cost analysis)
- Critical analysis of statistical fallacies (base-year normalization)

---

**Writing Instructions:**
- Use a professional but engaging tone suitable for a data science portfolio
- Emphasize the methodological rigor (especially the Scale Fallacy demonstration)
- Discuss the unexpected convergence finding and what it reveals about post-pandemic inflation
- Highlight policy implications: even though current gap is small, the 2016-2020 period shows 
  students bore higher inflation burden during critical enrollment years
- Frame this as demonstrating advanced statistical literacy (recognizing when official metrics 
  don't capture demographic-specific experiences)
- Include a "Future Research" section suggesting wage growth analysis to determine if students 
  maintained purchasing power during the high-inflation period
