# Data Wrangling & Engineering Pipeline

## Objective
Engineered a production-ready feature matrix from a deliberately chaotic HR dataset by diagnosing missingness mechanisms, applying conditional imputation, and resolving structural encoding failures that would otherwise invalidate econometric estimation.

## Methodology
- **Visual Missingness Forensics:** Deployed `missingno` matrix visualizations to identify structural alignment between missing `bonus_pay` and `performance_rating` fields, diagnosing a Missing at Random (MAR) mechanism rather than MCAR or MNAR
- **Conditional Median Imputation:** Imputed missing `base_salary` values using within-group medians grouped by department, preserving variance structure across organizational units rather than collapsing to a global mean
- **Dummy Variable Trap Analysis:** Demonstrated perfect multicollinearity failure by generating *k* binary indicator columns alongside an intercept term, producing a singular design matrix that causes OLS estimation to break down
- **Reference Class Encoding (k-1 methodology):** Resolved multicollinearity by dropping the first category via `drop_first=True`, establishing an implicit reference class against which all remaining department coefficients are interpreted
- **Target Encoding for High-Cardinality Features:** Compressed an 800-level `office_zip` variable into a single continuous vector representing mean salary by ZIP code using `category_encoders.TargetEncoder`, eliminating the sparsity and overfitting risk of one-hot encoding at scale

## Key Findings
Successfully transformed a structurally compromised dataset into a valid econometric input matrix. Missingness was confirmed as MAR and addressed without distorting departmental salary distributions. The Dummy Variable Trap was reproduced intentionally and resolved through proper reference class specification. High-cardinality geographic encoding was reduced from 800 sparse binary columns to a single dense continuous feature, substantially improving model tractability without sacrificing geographic salary signal.

**Tools:** Python, pandas, NumPy, statsmodels, missingno, category_encoders
