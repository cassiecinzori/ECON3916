# Clustering World Economies with K-Means & PCA

**Objective:** Applied unsupervised machine learning to World Bank development data to identify natural groupings among world economies and evaluate how well data-driven clusters recover expert income classifications.

## Methodology

- Fetched 10 World Development Indicators for ~160 countries via `wbgapi`, retaining countries with at least 7 of 10 available indicators and imputing remaining gaps with column medians
- Standardized all features using `StandardScaler` (mean=0, std=1) to ensure equal contribution to Euclidean distance calculations in K-Means
- Fit K-Means (K=4, `k-means++` initialization, `random_state=42`) and projected the 10-dimensional feature matrix to 2D via PCA for visual cluster inspection
- Evaluated K=2 through K=10 using the elbow method (WCSS/inertia) and mean silhouette score to identify optimal cluster count
- Cross-tabulated algorithmic cluster assignments against World Bank official income classifications (Low, Lower-Middle, Upper-Middle, High) to assess alignment
- Applied the full pipeline to California Housing census tract data, labeling emergent clusters with economically meaningful descriptions

## Key Findings

The elbow and silhouette diagnostics supported K=3 or K=4 as the natural cluster count in the World Bank data, with K=4 aligning substantively with the four-tier income classification. The cross-tabulation showed strong but imperfect correspondence: high- and low-income countries clustered with high fidelity, while middle-income economies showed more mixing, reflecting that GDP-adjacent indicators like life expectancy and internet penetration do not perfectly track GNI per capita thresholds. For California Housing, K=4 produced interpretable geographic-economic segments including an affluent coastal group, suburban middle class, urban working class, and rural low-income inland tracts.
