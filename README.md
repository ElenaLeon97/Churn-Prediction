# Predicting Customer Churn for a Dutch Energy Supplier

## Table of Contents

- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Cleaning/Preparation](#data-cleaningpreparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [OLS Model Summary](#ols-model-summary)
- [Results/Findings](#resultsfindings)
- [Recommendations](#recommendations)
- [Limitations](#limitations)
- [References](#references)

### Project Overview
---

This project investigates the drivers of customer churn in the energy sector and develops predictive models to identify customers at high risk of leaving. Using machine learning techniques and statistical analysis, the goal is to improve customer retention for a Dutch energy supplier.

### Data Sources
---

- **Customer records** with contract details, usage history, demographics
- **Electricity and gas consumption data** (yearly)
- Derived features: `Startchannel_dummy`, `Email_list`, `Switching_costs`, `Both_services`

### Tools
---

- **R** (for modeling, regression, and decision trees)
- **Machine learning models**: Logistic Regression, Stepwise Regression, Decision Trees, Bagging, Boosting, Random Forest

### Data Cleaning/Preparation
---

- Created dummy variables (e.g., `Startchannel_dummy`)
- Checked for missing values (none found)
- Identified and capped outliers using IQR method (Income, Gas/Electricity usage)
- Retained borderline demographic values (e.g., age < 18, > 100)

### Exploratory Data Analysis
---

- Summarized key variables (e.g., age, income, contract length)
- Plotted distributions for usage and service types
- Conducted correlation analysis (e.g., `Churn ~ Contract_length`, `Gas_usage`)
- Investigated multicollinearity among predictors

### Data Analysis
---

Built multiple predictive models to classify churners vs. non-churners and compared performance using:
- **Hit Ratio**
- **Top Decile Lift**
- **Gini Coefficient**

### OLS Model Summary
---

```r
# Logistic Regression Model
glm(formula = Churn ~ Email_list + Startchannel_dummy + Electricity_usage + Both_services + Switching_costs, 
    family = binomial, data = dataA1)
```
- Startchannel_dummy and Email_list were significant predictors
- Both_services was not statistically significant
- Odds Ratios:
    Startchannel_dummy: +8.04%
    Email_list: +7.1%

### Results/Findings
---
1. Best Model: Boosting (Model 1)
2. Hit Ratio: 75.68%
3. Top Decile Lift: 1.5876
4. Gini Coefficient: 0.6719
5. Strongest predictors across models:
    - Electricity usage
    - Gas usage
    - Relationship length
    - Contract length
    - Switching costs
    - Email engagement
    - Start channel
6. Insights by model:
   - Stepwise: Identified additional useful variables like province
   - Bagging: Highlighted demographic predictors like income and age
   - Decision Tree: Useful for marketing segmentation (e.g., flexible contracts + high gas usage = churn risk)
   - Random Forest: Strong predictive power but lacks directional interpretation

### Recommendations
---
- Implement Boosting Model 1 in churn monitoring pipelines
- Focus retention efforts on:
  i. High gas/electricity users
  ii. Customers with flexible contracts
  iii. Those with short relationship history
- Tailor campaigns based on acquisition channel and email availability
- Revisit service bundling strategies to reduce churn

### Limitations
---
- Model performance may vary across time or external conditions (e.g., energy price shocks)
- Some variables (e.g., Both_services) had limited variance or skew
- Non-linear interactions not fully interpretable in tree ensembles
- High correlation between some variables may affect interpretability

*This project was developed as part of an academic data science course. Data was anonymized, and all analysis was conducted under responsible data use guidelines.*
