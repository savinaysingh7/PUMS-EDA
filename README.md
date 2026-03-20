# 📊 PUMS-EDA — American Community Survey Exploratory Data Analysis

> Uncovering socio-economic patterns in U.S. Census microdata through rigorous Python-driven EDA.

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-2.x-150458?logo=pandas&logoColor=white)
![License](https://img.shields.io/badge/license-Academic-green)
![Dataset](https://img.shields.io/badge/Dataset-ACS%202023%201--Year%20PUMS-blueviolet)
![Observations](https://img.shields.io/badge/Observations-6%2C868-informational)
![Features](https://img.shields.io/badge/Features-287%20→%2015%20selected-yellow)
![Status](https://img.shields.io/badge/status-Complete-brightgreen)

---

## 📋 Table of Contents

- [🌟 Overview](#-overview)
- [✨ Features](#-features)
- [🛠️ Tech Stack](#️-tech-stack)
- [📁 Project Structure](#-project-structure)
- [⚡ Quick Start](#-quick-start)
- [📖 Analysis Walkthrough](#-analysis-walkthrough)
- [📊 Key Findings](#-key-findings)
- [🔬 Statistical Tests](#-statistical-tests)
- [📈 Visualizations](#-visualizations)
- [🧪 Reproducing Results](#-reproducing-results)
- [📝 Dataset](#-dataset)
- [🚀 Future Scope](#-future-scope)
- [👤 Author](#-author)
- [🙏 References](#-references)

---

## 🌟 Overview

This project presents a comprehensive **Exploratory Data Analysis (EDA)** of the [American Community Survey (ACS) 2023 1-Year Public Use Microdata Sample (PUMS)](https://www.census.gov/programs-surveys/acs/microdata.html), released by the U.S. Census Bureau. Working with 6,868 individual records across 287 raw variables, the analysis systematically cleans, reduces, and interrogates this rich microdata to reveal patterns in income, education, employment, and demographics across the United States.

The goal is to demonstrate end-to-end data science best practices — from raw messy data to statistically validated insights — using Python's scientific stack. This work was completed as the INT375 (Data Science Toolbox: Python Programming) course project at **Lovely Professional University**.

---

## ✨ Features

- 🧹 **Multi-stage data cleaning pipeline** — drops replicate weight columns, replaces special PUMS codes (e.g., `poverty_ratio == 501`) with `NaN`, and removes columns exceeding a 90% missingness threshold
- 📉 **Dimensionality reduction** — intelligently narrows 287 raw columns to 15 analytically meaningful socio-economic features via principled feature selection
- 🔢 **Dual imputation strategy** — median imputation for skewed numerical variables (`total_income_12m`, `wage_income_12m`, `commute_time`) and mode imputation for categorical variables
- 📊 **9 publication-quality visualizations** — age distribution (KDE histogram), raw and log-transformed income distributions, age vs. income scatter, gender bar chart, income by education level (box plot), correlation heatmap, regional income comparison, and pairwise pair plot
- 📐 **Log transformation of income** — applies `log1p(x + 6501)` to handle negative incomes and extreme right-skew, producing a near-symmetrical distribution suitable for modeling
- 📏 **IQR-based outlier detection** — identifies 521 high-income outliers in `total_income_12m` with bounds `[-44,687.50, +112,612.50]`; surfaces top outliers up to $787,000
- 🧮 **NumPy statistical operations** — vectorized mean, std, range, and z-score normalization on age data
- 🔬 **Welch's T-Test** — compares male vs. female mean income (t=9.794, p<0.001), confirming a statistically significant gender income gap
- 🔬 **Chi-Squared Test** — tests independence of employment status and gender (χ²=123.537, df=5, p<0.001), revealing a significant association
- 🔬 **Shapiro-Wilk Test** — rejects normality of age distribution (W=0.965, p<0.001)
- 🔬 **A/B Test** — compares income between Northeast (Region 1) and West (Region 4) using Welch's t-test
- 🔍 **VIF analysis** — checks multicollinearity across 4 numerical predictors; `total_income_12m` VIF ≈ 5.1, `wage_income_12m` VIF ≈ 4.2 — acceptable for regression use
- 💾 **Cleaned dataset export** — saves the final 6,868 × 15 imputed dataset as `census_data_cleaned.csv` for downstream modeling

---

## 🛠️ Tech Stack

| Category | Library | Version | Purpose |
|---|---|---|---|
| Data Manipulation | `pandas` | 2.x | DataFrame operations, missing value handling, groupby analysis |
| Numerical Computing | `numpy` | 1.x | Vectorized stats, array operations, log transforms |
| Visualization | `matplotlib` | 3.x | Base plotting engine for all figures |
| Visualization | `seaborn` | 0.x | Statistical plots — histplots, boxplots, heatmaps, pairplots, countplots |
| Statistical Testing | `scipy.stats` | 1.x | Welch's t-test (`ttest_ind`), chi-squared (`chi2_contingency`), Shapiro-Wilk (`shapiro`) |
| Multicollinearity | `statsmodels` | 0.x | Variance Inflation Factor (`variance_inflation_factor`) |
| Runtime | `Jupyter Notebook` | — | Interactive analysis environment with `%matplotlib inline` |

---

## 📁 Project Structure

```
PUMS-EDA/
├── eda.ipynb                                    # Main analysis notebook (68 cells)
├── census_data.csv                              # Raw ACS 2023 PUMS dataset (6,868 × 287)
├── census_data_cleaned.csv                      # Cleaned & imputed output (6,868 × 15)
├── INT375_EDA_Project_Report_Savinay_Singh.pdf  # Full project report (PDF)
├── INT375_EDA_Project_Report_Savinay_Singh.docx # Full project report (Word)
├── ACS2023_PUMS_README.pdf                      # Official U.S. Census Bureau PUMS documentation
├── original dataset/
│   └── psam_p02.csv                             # Original PUMS person file for Puerto Rico (state 02)
└── README.md                                    # This file
```

### Notebook Structure (`eda.ipynb` — 68 cells)

```
Cell 1–2    │ Library imports & plot style configuration
Cell 3–10   │ Data loading, shape inspection, .info(), .head(), missing value audit
Cell 11–14  │ Column classification (categorical < 20 unique values / numerical ≥ 20) + .describe()
Cell 15–20  │ Special code detection (poverty_ratio=501, migration_puma_area=70000) → NaN replacement
Cell 21–22  │ Column-level missingness (90% threshold drop: 287 → 196 columns)
Cell 23–26  │ Feature selection (196 → 15 key columns) + row-level missingness filter
Cell 27–44  │ Univariate & bivariate visualizations (8 plots)
Cell 45–46  │ Median/mode imputation + cleaned CSV export
Cell 47–48  │ NumPy descriptive statistics & age z-score normalization
Cell 49–52  │ IQR outlier detection & box plot
Cell 53–56  │ Welch's T-Test (gender income gap) + Chi-Squared (employment × gender)
Cell 57–58  │ VIF multicollinearity analysis
Cell 59–60  │ Shapiro-Wilk normality test for age
Cell 61–68  │ A/B test (regional income) + pair plot of numerical variables
```

---

## ⚡ Quick Start

### Prerequisites

```bash
Python >= 3.8
pip >= 21.x
Jupyter Notebook or JupyterLab
```

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/savinaysingh7/PUMS-EDA.git
cd PUMS-EDA

# 2. (Recommended) Create a virtual environment
python -m venv venv
source venv/bin/activate        # macOS/Linux
venv\Scripts\activate           # Windows

# 3. Install all dependencies
pip install pandas numpy matplotlib seaborn scipy statsmodels jupyter
```

### Running the Analysis

```bash
# Launch Jupyter Notebook
jupyter notebook eda.ipynb

# OR use JupyterLab
jupyter lab eda.ipynb
```

Then run all cells sequentially via **Kernel → Restart & Run All** to reproduce the complete analysis.

> **Note:** `census_data.csv` must be present in the same directory as `eda.ipynb`. The notebook will automatically generate `census_data_cleaned.csv` upon execution of Cell 46.

---

## 📖 Analysis Walkthrough

The notebook follows a strict, reproducible 7-stage pipeline:

### Stage 1 — Data Loading & Initial Audit
Loads `census_data.csv` into a Pandas DataFrame (6,868 rows × 287 columns). Runs `.info()`, `.head()`, and `.isnull().sum()` to surface the data landscape: a mix of `float64` (84 cols), `int64` (118 cols), and `object` (4 cols) types, with 86 columns containing at least one missing value.

### Stage 2 — Initial Cleaning
Programmatically identifies and drops all replicate weight columns (names containing `'weight_replicate'`), which are used only for variance estimation — out of scope for this point-estimate EDA.

### Stage 3 — Special Code Handling
Inspects high-frequency values in `poverty_ratio` and `migration_puma_area`. Replaces PUMS special codes (`501` → Not Applicable in poverty ratio; `70000` → Not Applicable in migration PUMA) with `np.nan`, preventing them from distorting descriptive statistics.

### Stage 4 — Dimensionality Reduction
Calculates per-column missingness percentage. Drops any column exceeding the **90% missing threshold** (e.g., `naturalization_year` at 96.7%, `grandcare_duration` at 98.3%), reducing the column count from 287 to 196.

### Stage 5 — Feature Selection
Selects 15 theoretically motivated variables for a focused socio-economic profile:

| Variable | Type | Description |
|---|---|---|
| `age_years` | Numerical | Individual's age (0–90) |
| `gender` | Categorical | 1 = Male, 2 = Female |
| `education_level` | Ordinal | ACS education code 1–24 (16 = Bachelor's) |
| `total_income_12m` | Numerical | Total personal income, past 12 months ($) |
| `wage_income_12m` | Numerical | Wage/salary income, past 12 months ($) |
| `employment_status_code` | Categorical | Employment status (1 = Employed) |
| `census_region` | Categorical | 1=NE, 2=MW, 3=South, 4=West |
| `race_detail_2_3` | Categorical | Detailed race code |
| `citizenship_status` | Categorical | Citizenship/nativity |
| `disability_status` | Categorical | Disability flag |
| `marital_status` | Categorical | Marital status code |
| `commute_time` | Numerical | Travel time to work (minutes) |
| `health_ins_coverage` | Categorical | Health insurance coverage flag |
| `state_code` | Categorical | U.S. state FIPS code |
| `puma_area` | Categorical | Public Use Microdata Area code |

### Stage 6 — Imputation
Applies **median imputation** for `age_years`, `total_income_12m`, `wage_income_12m`, `commute_time`, `education_level` (robust to the observed right-skew and outliers). Applies **mode imputation** for all remaining categorical variables. Result: a complete 6,868 × 15 DataFrame with zero missing values.

### Stage 7 — Statistical Testing & Export
Runs all hypothesis tests, VIF analysis, and pairwise visualizations on the imputed subset. Exports the cleaned dataset as `census_data_cleaned.csv`.

---

## 📊 Key Findings

### Income Distribution
- **Heavily right-skewed**: Mean income ($47,384) far exceeds median ($30,000), pulled upward by 521 IQR-detected outliers reaching up to **$787,000**
- Log transformation (`log1p(x + 6501)`) substantially improves symmetry, making the distribution viable for linear modeling

### Age Distribution
- Wide age diversity spanning **0 to 90 years**, mean ≈ 38.87, std ≈ 23.27
- Shapiro-Wilk test (W=0.965, p<0.001) confirms the distribution is **not normal**

### Education & Income
- Box plots reveal a **clear positive monotonic trend**: median income rises consistently with education level (code 1–24)
- Higher education levels also show wider income variance and more extreme outliers

### Gender & Income
- Welch's T-Test: **t = 9.794, p < 0.001** → statistically significant income gap between males and females in this sample
- Chi-Squared Test: **χ² = 123.537, p < 0.001** → gender and employment status are not independent

### Correlation Structure

| Variable Pair | Pearson r |
|---|---|
| `total_income_12m` ↔ `wage_income_12m` | **0.81** (strong) |
| `age_years` ↔ `total_income_12m` | 0.16 (weak) |
| `commute_time` ↔ `total_income_12m` | 0.088 (negligible) |
| `age_years` ↔ `wage_income_12m` | -0.036 (negligible) |

### Multicollinearity (VIF)

| Feature | VIF |
|---|---|
| `age_years` | 1.96 — no collinearity |
| `total_income_12m` | 5.11 — moderate (expected, correlated with wages) |
| `wage_income_12m` | 4.17 — moderate |
| `commute_time` | 1.56 — no collinearity |

---

## 🔬 Statistical Tests

### Welch's T-Test — Gender Income Gap
```
H₀: Mean income of males = Mean income of females
H₁: Mean income of males ≠ Mean income of females

Result: T-statistic = 9.794, P-value ≈ 0.000
Decision: Reject H₀ (p < 0.05) → Statistically significant income difference by gender
```

### Chi-Squared Test — Employment Status × Gender
```
H₀: Employment status and gender are independent
H₁: Employment status and gender are associated

Result: χ² = 123.537, df = 5, P-value ≈ 0.000
Decision: Reject H₀ → Significant association exists between gender and employment status
```

### Shapiro-Wilk Test — Age Normality
```
H₀: age_years is normally distributed
H₁: age_years is not normally distributed

Result: W = 0.965, P-value ≈ 0.000
Decision: Reject H₀ → Age distribution significantly deviates from normality
```

### A/B Test — Regional Income (Northeast vs. West)
```
H₀: Mean income in Region 1 (NE) = Mean income in Region 4 (West)

Result: T-statistic = nan, P-value = nan
Note: Test inconclusive due to insufficient data in one or both regional groups after subsetting
```

---

## 📈 Visualizations

| # | Figure | Description |
|---|---|---|
| 1 | Age Distribution | Histogram + KDE showing 0–90 age range with mean/median markers |
| 2 | Total Income Distribution | Right-skewed histogram (0–$800,000) with mean/median lines |
| 3 | Log-Transformed Income | `log1p(x + 6501)` histogram showing improved symmetry |
| 4 | Age vs. Total Income | Scatter plot — no strong linear trend; wider spread for middle-aged groups |
| 5 | Gender Distribution | Count plot showing near-balanced male/female split (~3,650 vs. ~3,150) |
| 6 | Income by Education Level | Box plot across 24 education codes — clear positive trend |
| 7 | Correlation Heatmap | Pearson r matrix for `age_years`, `total_income_12m`, `wage_income_12m`, `commute_time` |
| 8 | Income Outlier Box Plot | Box plot of `total_income_12m` showing 521 outliers above $112,612.50 |
| 9 | Regional Income with 95% CI | Bar plot comparing mean income across census regions |

All figures are generated inline in `eda.ipynb` using `seaborn` with `whitegrid` style and `matplotlib` as the backend.

---

## 🧪 Reproducing Results

All results are fully reproducible by running `eda.ipynb` from top to bottom. There are no random seeds required, as no stochastic operations are used in this analysis.

```python
# Verify cleaned dataset after running notebook
import pandas as pd
df = pd.read_csv('census_data_cleaned.csv')
print(df.shape)          # Expected: (6868, 15)
print(df.isnull().sum()) # Expected: all zeros
print(df.dtypes)
```

Expected cleaned column list:
```
age_years, gender, education_level, total_income_12m, employment_status_code,
census_region, race_detail_2_3, citizenship_status, disability_status, marital_status,
wage_income_12m, commute_time, health_ins_coverage, state_code, puma_area
```

---

## 📝 Dataset

### Source
**American Community Survey (ACS) 2023 1-Year PUMS**
- Publisher: U.S. Census Bureau
- Access: [https://www.census.gov/programs-surveys/acs/microdata/access.html](https://www.census.gov/programs-surveys/acs/microdata/access.html)
- Documentation: [https://www.census.gov/programs-surveys/acs/microdata/documentation.html](https://www.census.gov/programs-surveys/acs/microdata/documentation.html)

### Important Notes on Weighting
The ACS PUMS is a **survey, not a census**. To produce population-representative estimates, the **Person Weight (`PWGTP`)** must be applied. This analysis deliberately omits survey weights, as the focus is on exploring patterns within the sample itself. Conclusions should not be generalized to the U.S. population without applying weights and calculating margins of error.

| Property | Value |
|---|---|
| File used | `census_data.csv` (derived from `psam_p02.csv`) |
| Raw dimensions | 6,868 rows × 287 columns |
| Analysis dimensions | 6,868 rows × 15 columns |
| Survey year | 2023 (1-Year estimates) |
| Geography | PUMA-level (state FIPS code 02 — Alaska/Puerto Rico) |
| Confidentiality | Anonymized via Census Bureau data swapping |

---

## 🚀 Future Scope

1. **Apply survey weights** (`PWGTP`) to generate statistically valid population-level estimates with margins of error, enabling comparison with official Census Bureau published tables

2. **Predictive modeling** — build income regression models using education, age, gender, and region as predictors; explore quantile regression to capture the full income distribution rather than just the mean

3. **Subgroup / stratified analysis** — examine whether the education–income relationship holds uniformly across race categories (`race_detail_2_3`) and citizenship statuses

4. **Outlier impact assessment** — apply winsorization or robust regression techniques to quantify the sensitivity of results to the 521 high-income outliers

5. **Expanded feature set** — reintroduce industry and occupation codes (`soc_occupation`) for richer employment pattern analysis

6. **Geospatial analysis** — leverage `state_code` and `puma_area` for geographic income disparity mapping, potentially integrating with external TIGER/Line shapefiles

---

## 👤 Author

**Savinay Singh**
Registration No. 12308126 | B.Tech CSE (K23DW)
Lovely Professional University, Phagwara, Punjab

- GitHub: [@savinaysingh7](https://github.com/savinaysingh7)

*Submitted as the INT375 (Data Science Toolbox: Python Programming) Project — January–April 2025*
*Guided by: Vikash Mangotra (UID: 31488), Assistant Professor, Discipline of CSE/IT*

---

## 🙏 References

1. U.S. Census Bureau, "ACS PUMS," [census.gov](https://www.census.gov/programs-surveys/acs/microdata.html)
2. U.S. Census Bureau, "PUMS Documentation," [census.gov](https://www.census.gov/programs-surveys/acs/microdata/documentation.html)
3. Pandas Development Team, "pandas: powerful Python data analysis toolkit," Zenodo, 2020
4. C. R. Harris et al., "Array programming with NumPy," *Nature*, vol. 585, pp. 357–362, 2020
5. J. D. Hunter, "Matplotlib: A 2D graphics environment," *Comput. Sci. Eng.*, vol. 9, no. 3, pp. 90–95, 2007
6. M. L. Waskom, "Seaborn: statistical data visualization," *J. Open Source Softw.*, vol. 6, no. 60, p. 3021, 2021
7. P. Virtanen et al., "SciPy 1.0: Fundamental algorithms for scientific computing in Python," *Nat. Methods*, vol. 17, pp. 261–272, 2020
8. S. Seabold and J. Perktold, "statsmodels: Econometric and statistical modeling with Python," *9th Python in Science Conference*, 2010

---

<p align="center">Made with 🐍 Python · 📓 Jupyter · 📊 Seaborn · Built for INT375 @ LPU</p>