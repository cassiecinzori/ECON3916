# Descriptive Statistics & Anomaly Detection

A comparative analysis of manual statistical methods versus machine learning approaches for detecting outliers in California housing data, with a focus on robust statistical measures and economic inequality metrics.

## Overview

This project investigates the reliability of different statistical measures and anomaly detection techniques using the California Housing dataset. Through both traditional statistical methods (IQR) and modern machine learning (Isolation Forest), the analysis demonstrates the "breakdown effect" of the mean versus the median and explores economic inequality patterns in housing markets.

## Key Features

**Statistical Forensics**
- IQR-based outlier detection using Tukey fences
- Comparative analysis of mean vs. median robustness to outliers
- Calculation of "inequality wedge" (mean-median gap) as an inequality metric

**Machine Learning Detection**
- Isolation Forest implementation for multivariate anomaly detection
- Comparison of statistical vs. algorithmic approaches
- Visualization of outlier distributions across income and housing features

**Volatility Analysis**
- Standard deviation vs. MAD (Median Absolute Deviation) comparison
- Separate analysis of "normal" and "outlier" populations
- Distribution analysis of core market vs. tail segments

## Technologies

- **Python 3.x**
- **Libraries**: pandas, scikit-learn, seaborn, matplotlib, numpy

## Key Findings

- The mean is **~23x more sensitive** to outliers than the median for income data
- Isolation Forest detected **5% contamination** across multivariate features
- Outlier populations show significantly larger inequality wedges, indicating asymmetric distributions
- MAD provides more robust volatility estimates than standard deviation in skewed data

## Usage

```python
# Clone repository
git clone [your-repo-url]

# Install dependencies
pip install pandas scikit-learn seaborn matplotlib numpy

# Run analysis
python descriptive_statistics_&_anomaly_detection.py
```

## Dataset

The analysis uses the California Housing dataset from scikit-learn, which contains 20,640 observations with features including:
- Median income
- House age
- Average rooms/bedrooms
- Population
- Median house value (capped at $500k)

## Author

**Cassandra Cinzori**  
Data Science & Economics | Northeastern University

---

*Part of ECON 3916: Statistical & Machine Learning for Economics coursework*
