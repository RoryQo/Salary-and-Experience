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

```
model = lm(salary ~ years, data = salary)
```

5. **Residual Analysis (Untransformed)**: Predicted values and jackknife residuals are calculated from the model. A residual plot is created to assess the fit of the model. In this plot, patterns may emerge that indicate non-linearity, such as a funnel shape, suggesting that the relationship between salary and years of employment is not purely linear. Additionally, heteroskedasticity may be present, where the variability of residuals increases with the level of predicted salary.

6. **Transformation**: The salary variable is transformed using a natural log transformation to address the identified issues of non-linearity and heteroskedasticity.

```
salary$log_salary = log(salary$salary)
```

7. **Scatterplot for Transformed Data**: A scatterplot is generated to visualize the relationship between years of employment and the natural log of salary, which provides a more linear relationship.

<br>
<br>
<br>
<div style="display: flex; justify-content: space-between;">

  <img src="https://github.com/RoryQo/Salary-and-Experience/raw/main/PreScatter.jpg" alt="Pre-Transformation Scatter Plot" style="width: 400px;">

  <img src="https://github.com/RoryQo/Salary-and-Experience/raw/main/PostScat.jpg" alt="Post-Transformation Scatter Plot" style="width: 400px;">

</div>

<br>
<br>
<br>

9. **Model Fitting (Transformed)**: A new linear regression model is fitted using the transformed salary data to predict the natural log of salary based on years of employment. The coefficients from this model indicate the percentage change in salary for each additional year of experience.

```
tr_model = lm(log(salary) ~ years, data = salary)
```

10. **Residual Analysis (Transformed)**: Predictions and residuals from the transformed model are calculated, and a residual plot is created to evaluate the fit. The residuals should be more evenly distributed around zero, indicating a better model fit without patterns of non-linearity or heteroskedasticity.
<br>
<br>
<br>

<div style="display: flex; justify-content: space-between;">

  <img src="https://github.com/RoryQo/Salary-and-Experience/raw/main/PreResid.jpg" alt="Pre-Transformation Residual Plot" style="width: 400px;">

  <img src="https://github.com/RoryQo/Salary-and-Experience/raw/main/PostResid.jpg" alt="Post-Transformation Residual Plot" style="width: 400px;">

</div>

<br>
<br>
<br>

11. **Model Summaries**: Summaries of both the untransformed and transformed models are generated. The outputs include:
   - **Coefficients**:
       - **Intercept**: 9.980798
       - **Years**: 0.077595
         - This value represents the estimated percentage change in salary for each additional year of experience. Specifically, for each additional year of employment, the salary is expected to increase by about 7.76% (since \( e^{0.077595} \approx 1.080\)).
     - **R-squared**: 0.9244
       - This indicates that approximately 92.44% of the variability in the natural log of salary can be explained by years of employment. This improvement suggests that the log transformation has helped in capturing the relationship more effectively than the untransformed model that captured 81% of the relationship.
     - **P-values**:
       - **Intercept**: < 2e-16 (highly significant)
       - **Years**: < 2e-16 (highly significant)

## Conclusion

By applying a natural log transformation to the salary variable, these assumptions were better satisfied in the transformed model. The R-squared value increased to approximately 92.44%, indicating a substantial improvement over the 81.1% in the untransformed model.

In the transformed model, the coefficient for years of employment is about 0.0776, with a standard error of approximately 0.0029. This suggests that each additional year of employment is associated with an approximate 7.6% increase in salary, and the small standard error indicates a precise estimate. The residual standard error decreased to 0.2076, reflecting tighter clustering of the residuals around the predicted values. The p-value for the years coefficient is less than 2e-16, confirming a statistically significant relationship.

Overall, the log transformation enhanced the model's ability to accurately reflect the relationship between years of employment and salary, addressing issues of non-linearity and heteroskedasticity that were evident in the untransformed model.

## License
This code is intended for educational purposes. Proper attribution is appreciated if used in any publications or presentations.
