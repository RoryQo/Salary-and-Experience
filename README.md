# Salary and Years of Experience Analysis

## Table of Contents
- [Overview](#overview)
- [Requirements](#requirements)
- [Data](#data)
- [Methodology](#methodology)
- [Conclusion](#conclusion)
- [License](#license)

## Overview
This script analyzes the relationship between salary and years of employment using linear regression models, both with the original salary data and after applying a natural log transformation. It includes visualizations such as scatterplots and residual plots.

## Requirements
- R (version 4.2.3 or later)
- R package: `ggplot2`

## Data
The script requires a CSV file named `salary.csv` that should include the following columns:
- `years`: Years of employment.
- `salary`: Salary values.

## Methodology

2. **Scatterplot Creation**: A scatterplot is generated to visualize the relationship between years of employment and salary. Points are styled with an outlined color for clarity.

3. **Model Fitting (Untransformed)**: A linear regression model is fitted using the untransformed salary data. The model predicts salary based on years of employment, providing coefficients that indicate the expected change in salary for each additional year of experience.

4. **Residual Analysis (Untransformed)**: Predicted values and jackknife residuals are calculated from the model. A residual plot is created to assess the fit of the model. In this plot, patterns may emerge that indicate non-linearity, such as a funnel shape, suggesting that the relationship between salary and years of employment is not purely linear. Additionally, heteroskedasticity may be present, where the variability of residuals increases with the level of predicted salary.

5. **Transformation**: The salary variable is transformed using a natural log transformation to address the identified issues of non-linearity and heteroskedasticity.

```
salary$log_salary = log(salary$salary)
```

7. **Scatterplot for Transformed Data**: A scatterplot is generated to visualize the relationship between years of employment and the natural log of salary, which provides a more linear relationship.

8. **Model Fitting (Transformed)**: A new linear regression model is fitted using the transformed salary data to predict the natural log of salary based on years of employment. The coefficients from this model indicate the percentage change in salary for each additional year of experience.

```
tr_model = lm(log(salary) ~ years, data = salary)
```

10. **Residual Analysis (Transformed)**: Predictions and residuals from the transformed model are calculated, and a residual plot is created to evaluate the fit. The residuals should be more evenly distributed around zero, indicating a better model fit without patterns of non-linearity or heteroskedasticity.



11. **Model Summaries**: Summaries of both the untransformed and transformed models are generated. The outputs include:
   - **Coefficients**: Estimates that show the relationship between the predictor and response variables.
   - **R-squared Values**: Indicators of the proportion of variance explained by the model, with higher values suggesting better explanatory power.
   - **P-values**: Assess the statistical significance of the coefficients, with values less than 0.05 indicating strong evidence against the null hypothesis.

## Conclusion
The analysis reveals a clear relationship between salary and years of employment, with the initial model demonstrating potential non-linear patterns and signs of heteroskedasticity. The natural log transformation improves the fit of the model and provides more reliable estimates. The transformed model outputs indicate a statistically significant relationship, suggesting that as years of experience increase, salary also increases, both in absolute terms and on a percentage basis when using the log transformation. The residual plots confirm that the transformed model addresses the issues identified in the untransformed model, leading to a more robust analysis.

Overall, this approach underscores the importance of addressing non-linearity and heteroskedasticity in regression analysis to ensure that model assumptions are met and to enhance the understanding of salary determinants. Future work could involve exploring additional variables or more complex modeling techniques to further refine the analysis.

## License
This code is intended for educational purposes. Proper attribution is appreciated if used in any publications or presentations.
