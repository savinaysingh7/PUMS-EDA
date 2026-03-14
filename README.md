# PUMS EDA (Public Use Microdata Sample - Exploratory Data Analysis)

## Project Overview
This project presents an in-depth Exploratory Data Analysis (EDA) of the Public Use Microdata Sample (PUMS) dataset from the US Census Bureau. The analysis is conducted as part of the INT375 course project.

## Repository Contents
- **`eda.ipynb`**: The main Jupyter Notebook containing the complete exploratory data analysis, visualizations, and statistical testing.
- **`census_data.csv`**: The primary dataset used for the analysis.
- **`INT375_EDA_Project_Report_Savinay_Singh.pdf` / `.docx`**: The final detailed project reports summarizing the findings.
- **`original dataset/`**: Directory containing the original data files.

## Analysis Highlights
The Jupyter Notebook (`eda.ipynb`) covers the following key stages of analysis:

1. **Data Cleaning & Preprocessing**: 
   - Handling missing values and replacing special codes.
   - Dropping columns/rows with excessive missing data. 
   - Feature typing and classifying columns (categorical vs. numerical).
   - Missing value imputation (median for numerical and mode for categorical features).

2. **Exploratory Visualizations**:
   - Univariate distributions: Age, Total Income, Log-Transformed Income, Gender, and Employment Status.
   - Bivariate & Multivariate distributions: Age vs. Total Income, Income by Education Level, Income by Census Region.
   - Visualizing pairwise relationships and correlation heatmaps for numerical variables.

3. **Outlier Detection**: 
   - Identifying and visualizing anomalies in total income using the Interquartile Range (IQR) method.

4. **Statistical Hypothesis Testing**:
   - **Welch's T-Test**: Comparing total income between males and females.
   - **Chi-Squared Test**: Examining the relationship between employment status and gender.
   - **Shapiro-Wilk Test**: Checking the normality of the age variables.
   - **A/B Testing**: Evaluating differences in income across different census regions.
   - **Variance Inflation Factor (VIF)**: Accessing multicollinearity among numerical features.

## Required Libraries
To reproduce the analysis, ensure you have the following Python libraries installed:
- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`
- `scipy`
- `statsmodels` (for VIF computation)

## How to Run
1. Clone or download this repository.
2. Ensure you have the required libraries installed in your Python environment.
3. Open `eda.ipynb` using Jupyter Notebook, JupyterLab, or VS Code.
4. Execute the cells sequentially to reproduce the data cleaning, visualizations, and statistical tests.
