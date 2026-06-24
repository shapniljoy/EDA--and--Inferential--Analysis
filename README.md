[eda-analysis-report.md](https://github.com/user-attachments/files/29311066/eda-analysis-report.md)
# Exploratory Data Analysis Report: Global Cancer Patients 2015–2024

---

## Table of Contents

1. [Dataset Overview](#dataset-overview)
2. [Methodology](#methodology)
3. [Theme 1: Distribution of Patient Demographics and Clinical Variables](#theme-1-distribution-of-patient-demographics-and-clinical-variables)
4. [Theme 2: Relationship Between Risk Factors and Cancer Severity](#theme-2-relationship-between-risk-factors-and-cancer-severity)
5. [Theme 3: Early-Stage Detection Across Cancer Types](#theme-3-early-stage-detection-across-cancer-types)
6. [Theme 4: Key Predictors of Cancer Severity and Survival Years](#theme-4-key-predictors-of-cancer-severity-and-survival-years)
7. [Theme 5: Economic Burden of Cancer Treatment](#theme-5-economic-burden-of-cancer-treatment)
8. [Theme 6: Cancer Stage and Its Effect on Treatment Cost and Survival](#theme-6-cancer-stage-and-its-effect-on-treatment-cost-and-survival)
9. [Theme 7: Interaction Effect of Genetic Risk and Smoking on Cancer Severity](#theme-7-interaction-effect-of-genetic-risk-and-smoking-on-cancer-severity)
10. [Summary of Key Findings](#summary-of-key-findings)

---

## Dataset Overview

The dataset used in this analysis is the **Global Cancer Patients 2015–2024** dataset sourced from Kaggle. It contains patient-level records spanning a decade across **10 countries**, capturing a wide range of demographic, lifestyle, clinical, and economic variables. The key variables included in the analysis are:

| Variable | Type | Description |
|---|---|---|
| `Patient_ID` | Identifier | Unique patient identifier |
| `Age` | Numerical | Patient age in years |
| `Gender` | Categorical | Male, Female, Other |
| `Country_Region` | Categorical | 10 countries of patient origin |
| `Year` | Categorical/Ordinal | Year of record (2015–2024) |
| `Genetic_Risk` | Numerical | Standardized genetic risk score |
| `Air_Pollution` | Numerical | Standardized air pollution exposure score |
| `Alcohol_Use` | Numerical | Standardized alcohol use score |
| `Smoking` | Numerical | Standardized smoking intensity score |
| `Obesity_Level` | Numerical | Standardized obesity level score |
| `Cancer_Type` | Categorical | Type of cancer diagnosed |
| `Cancer_Stage` | Categorical | Stage of cancer at diagnosis |
| `Treatment_Cost_USD` | Numerical | Cost of treatment in USD |
| `Survival_Years` | Numerical | Years of patient survival |
| `Target_Severity_Score` | Numerical | Composite cancer severity score (primary target) |

---

## Methodology

The analysis follows a structured three-phase approach:

**Phase 1 — Descriptive Analysis (Univariate):** Each variable is examined individually for distributional shape, central tendency, spread, normality, and presence of outliers using histograms, KDE plots, boxplots, and Q-Q plots for numerical variables, and bar charts with pie charts for categorical variables.

**Phase 2 — Bivariate and Multivariate Analysis:** Relationships between pairs and combinations of variables are explored using scatter plots, regression plots, violin plots, strip plots, and heatmapped cross-tabulations. Statistical tests applied include Pearson and Spearman correlation, t-tests, one-way ANOVA, Chi-square tests for independence, and simple OLS linear regression.

**Phase 3 — Feature Importance via Random Forest:** A Random Forest Regressor (100 estimators) is trained on an 80/20 train-test split with standardized numerical features and label-encoded categorical features, and feature importances are extracted for both the `Target_Severity_Score` and `Survival_Years` target variables.

---

## Theme 1: Distribution of Patient Demographics and Clinical Variables

### Age

The age of patients in the dataset ranges from **20 to 89 years**, with a mean age of **54 years** and a standard deviation of **20 years**. The interquartile range spans Q1 = 37 to Q3 = 72, indicating that the middle 50% of patients fall within this range. The distribution is **uniform**, with roughly equal representation across all age groups. The Shapiro-Wilk test confirms the data is not normally distributed, and no outliers are detected via the IQR method.

### Gender

Gender is recorded across three categories: **Male, Female, and Other**. Each category accounts for approximately **32–33% of the total patient population**, indicating a near-perfect balance across groups. There are no missing values in this variable.

### Country/Region

The dataset covers **10 countries**. **Australia** has the highest number of patients at **5,092**, while all other countries are approximately equally represented, each contributing close to **10% of the total data**. The variance in country-level representation is very low, suggesting a balanced international sample.

### Risk Factor Variables

Five standardized risk factor variables — **Genetic_Risk, Air_Pollution, Alcohol_Use, Smoking**, and **Obesity_Level** — share nearly identical distributional properties. Each is **uniformly distributed** with a mean of approximately **5** and a standard deviation of approximately **2.88**. None of the variables contain outliers. The analyst notes that these five variables appear to have been collected on the same standardized scale, and that they may carry interaction effects on the primary target variable.

### Cancer Type and Cancer Stage

Both `Cancer_Type` and `Cancer_Stage` are categorical variables analyzed for frequency distribution. Their distributions are examined through bar charts and pie charts, revealing the relative representation of different cancer types and clinical stages within the dataset.

### Treatment Cost and Target Severity Score

Both `Treatment_Cost_USD` and `Target_Severity_Score` are continuous numerical variables. Their univariate distributions are examined using histograms, KDE plots, boxplots, and Q-Q plots as part of the descriptive phase, providing a baseline understanding of their spread and shape before relational analyses are conducted.

---

## Theme 2: Relationship Between Risk Factors and Cancer Severity

The five risk factors — Genetic_Risk, Air_Pollution, Alcohol_Use, Smoking, and Obesity_Level — are each examined in relation to the `Target_Severity_Score` using scatter plots, line charts, regression plots, Pearson and Spearman correlation tests, and simple OLS regression.

### Directional Relationship

A **consistent positive directional relationship** is observed between each of the five risk factors and the severity score. As any of the five risk factors increases, the severity score also increases.

### Correlation Strength

Both Pearson and Spearman correlation coefficients for the five risk factors against the severity score range from **approximately 0.25 to 0.48**. These values indicate **weak to moderate positive linear associations**. All correlations are statistically significant (p < 0.05), leading to rejection of the null hypothesis of no relationship in each case.

### Explained Variability

When simple OLS linear regression is run for each risk factor individually against the severity score, the R² values range from **6.32% to 23.47%**. This means that any single risk factor in isolation explains only a small fraction of the total variance in cancer severity. The analyst interprets this as evidence that the risk factors, while individually significant, do not individually account for the bulk of severity variation.

---

## Theme 3: Early-Stage Detection Across Cancer Types

### Cross-Tabulation of Cancer Stage and Cancer Type

A chi-square test of independence is applied to the cross-tabulation of `Cancer_Stage` and `Cancer_Type`. The resulting heatmap provides a visual breakdown of how patients with different cancer types are distributed across the various stages of diagnosis.

### Proportion of Early-Stage Detection

For each cancer type, the proportion of patients detected at **Stage 0 or Stage I** (the two earliest stages) is computed individually. This analysis quantifies how frequently each cancer type is identified at an early and potentially more treatable stage. The proportions are reported per cancer type, offering a comparative view of early detection rates across the spectrum of cancer diagnoses present in the dataset.

---

## Theme 4: Key Predictors of Cancer Severity and Survival Years

### Correlation Analysis

A combined Pearson and Spearman correlation matrix is constructed for the five risk factors against both `Target_Severity_Score` and `Survival_Years`. The key finding from this analysis is that **none of the five risk factors show a meaningful association with `Survival_Years`**. The analyst concludes that the existing set of covariates may be insufficient for predicting patient survival duration using standard correlation-based approaches.

### Random Forest Feature Importance — Target Severity Score

A Random Forest Regressor is trained to predict `Target_Severity_Score` using all available patient features excluding `Patient_ID`, `Treatment_Cost_USD`, and `Survival_Years`. The model achieves an **R² of approximately 76%** on the test set, indicating an acceptable level of predictive performance.

Feature importance scores reveal that the **top five predictors**, in descending order of importance, are:

1. Smoking
2. Genetic Risk
3. Alcohol Use
4. Air Pollution
5. Obesity Level

These five variables together account for **88% of the total feature importance**, making them the dominant drivers of cancer severity in this dataset. The remaining variables — including age, gender, country, year, cancer type, and cancer stage — contribute a combined 12%.

### Random Forest Feature Importance — Survival Years

When the same Random Forest framework is applied to predict `Survival_Years`, the model produces a **negative R² score**. This confirms the finding from the correlation analysis: the current set of covariates is **not suitable for predicting survival duration**. The analyst determines that the predictor set available in the dataset lacks the explanatory power needed for this outcome variable.

---

## Theme 5: Economic Burden of Cancer Treatment

### Treatment Cost by Gender

A comparison of `Treatment_Cost_USD` across gender groups using statistical testing reveals that **the median treatment cost is slightly higher for patients of "Other" gender** compared to Male and Female patients.

### Treatment Cost by Country

Significant variation in median treatment cost is observed across countries. **Pakistan** records the **lowest median treatment cost**, while **China and Germany** record the **highest median treatment costs**. A one-way ANOVA is applied to confirm the presence of statistically significant differences across country groups.

### Treatment Cost by Age Group

Patient ages are divided into four categories for this analysis:
- **Young**: ages 20–35
- **Middle-Aged**: ages 35–50
- **Old**: ages 50–65
- **Senior Citizen**: ages 65–89

Treatment costs are compared across these age groups. The distributional patterns are examined visually and statistically, revealing how economic burden varies across the patient lifecycle.

### Multivariate Analysis — Country × Gender

When treatment cost is examined simultaneously across country and gender:

- The **highest mean treatment cost** is observed in the **USA for patients of "Other" gender**.
- The **overall lowest** is in **Pakistan for female patients**.
- For **female** patients: lowest in Pakistan, highest in Germany.
- For **male** patients: lowest in Pakistan, highest in China.
- For **Other gender** patients: the lowest cost country is Brazil.

### Multivariate Analysis — Country × Age Group

When treatment cost is analyzed across country and age group:

- **Germany** records the highest mean cost for **young** patients, while **India** records the lowest for **middle-aged** patients.
- **Middle-aged** patients generally face lower treatment costs across countries.
- For **Senior Citizens**: cost is highest in **Australia** and lowest in **Germany**.
- For **Old** patients: cost is highest in **India** and lowest in **Australia**.
- For **Middle-Aged** patients: cost is highest in **Brazil**.
- For **Young** patients: cost is lowest in **India**.

---

## Theme 6: Cancer Stage and Its Effect on Treatment Cost and Survival

### Treatment Cost Across Cancer Stages

The mean `Treatment_Cost_USD` is computed for each cancer stage and is found to be **approximately $52,000** across all stages, with negligible variation between them. This finding is visually confirmed through bar plots and box plots comparing cost distributions across Stage 0, Stage I, Stage II, Stage III, and Stage IV.

### Survival Years Across Cancer Stages

Similarly, the mean `Survival_Years` is calculated per cancer stage and is found to be **approximately 5 years** consistently across all stages. The distributional analyses confirm that cancer stage, as captured in this dataset, does not produce a meaningful gradient in either treatment cost or survival duration.

---

## Theme 7: Interaction Effect of Genetic Risk and Smoking on Cancer Severity

### Construction of the Interaction Term

To examine whether higher genetic risk amplifies the negative effect of smoking on cancer severity, an interaction variable is constructed as the **product of `Genetic_Risk` and `Smoking`**. A square root transformation of this product is also applied and examined for distributional properties.

### OLS Regression with Interaction Term

An OLS regression model is specified as:

```
Target_Severity_Score ~ Genetic_Risk + Smoking + sqrt(Genetic_Risk × Smoking)
```

The model is estimated using `statsmodels`. The results show that the **p-value for the interaction term (sqrt of the product) is 0.668**, which is well above the conventional significance threshold of 0.05.

### Conclusion

The null hypothesis of no significant interaction effect is **not rejected**. The analysis concludes that there is **no statistically significant combined effect** of genetic risk and smoking on the cancer severity score. While both variables are individually important predictors (as confirmed in the feature importance analysis), their combined interaction term does not explain additional variance in severity beyond their individual contributions.

---

## Summary of Key Findings

| # | Theme | Key Finding |
|---|---|---|
| 1 | Demographics & Distributions | Age, gender, and country representation are highly balanced. The five risk factor variables share identical uniform distributions and standardized scales. |
| 2 | Risk Factors & Cancer Severity | All five risk factors have weak to moderate positive relationships with severity (r = 0.25–0.48), each individually explaining only 6.3–23.5% of variance. |
| 3 | Early-Stage Detection | The proportion of patients diagnosed at Stage 0 or Stage I varies by cancer type, with per-cancer-type proportions computed and compared. |
| 4 | Key Predictors | The top five predictors of cancer severity are Smoking, Genetic Risk, Alcohol Use, Air Pollution, and Obesity Level (88% combined importance). Survival Years cannot be predicted with the existing variables. |
| 5 | Economic Burden | Treatment costs vary significantly by country and gender. Pakistan consistently shows the lowest costs; China, Germany, and the USA show the highest depending on demographic group. Middle-aged patients incur generally lower costs. |
| 6 | Cancer Stage vs. Outcomes | Neither treatment cost (~$52,000) nor survival years (~5 years) differ meaningfully across cancer stages in this dataset. |
| 7 | Genetic Risk × Smoking Interaction | No significant interaction effect between genetic risk and smoking on cancer severity is found (p = 0.668). |

---

*Analysis conducted on the Global Cancer Patients 2015–2024 dataset. All statistical tests are conducted at a significance level of α = 0.05. Visualizations produced using Seaborn, Matplotlib, and Plotly. Feature importance estimates derived from a Random Forest Regressor (100 estimators, random_state=0).*
