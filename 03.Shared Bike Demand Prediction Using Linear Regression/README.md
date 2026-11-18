# Shared Bike Demand Prediction Using Linear Regression

## Overview

This project is an academic machine learning case study focused on
predicting daily shared-bike demand using multiple linear regression.

The objective is to identify factors that influence daily bike rentals
and build an interpretable regression model for demand prediction.

The analysis covers exploratory data analysis, categorical encoding,
feature selection, multiple linear regression, model evaluation,
multicollinearity analysis, residual analysis, and validation of
regression assumptions.

> **Project Type:** Academic / Machine Learning / Regression\
> **Domain:** Transportation / Shared Mobility\
> **Tools:** Python, Pandas, NumPy, Matplotlib, Seaborn, Statsmodels,
> Scikit-learn, Jupyter Notebook

------------------------------------------------------------------------

## Problem Statement

A bike-sharing provider wants to understand the factors affecting the
demand for shared bikes in the American market.

The business objectives are to determine which variables are significant
in predicting demand and how well those variables explain variations in
daily bike rentals.

The target variable is `cnt`, representing the total number of daily
bike rentals.

------------------------------------------------------------------------

## Objectives

The main objectives were to:

1.  Understand the structure and characteristics of the bike-sharing
    dataset.
2.  Perform exploratory data analysis to identify important demand
    patterns.
3.  Convert categorical variables into an appropriate representation for
    regression.
4.  Identify variables that significantly influence bike demand.
5.  Build a multiple linear regression model.
6.  Evaluate the model using the test-set R² score.
7.  Check multicollinearity using correlation analysis and VIF.
8.  Perform residual analysis.
9.  Validate key assumptions of linear regression.
10. Interpret the final model and identify influential predictors.

------------------------------------------------------------------------

## Dataset

The dataset contains **730 daily observations** covering two years of
bike-sharing activity.

  Variable       Description
  -------------- -----------------------------------
  `instant`      Record index
  `dteday`       Date
  `season`       Season of the year
  `yr`           Year indicator
  `mnth`         Month
  `holiday`      Whether the day was a holiday
  `weekday`      Day of the week
  `workingday`   Whether the day was a working day
  `weathersit`   Weather condition
  `temp`         Normalized temperature
  `atemp`        Normalized feeling temperature
  `hum`          Normalized humidity
  `windspeed`    Normalized wind speed
  `casual`       Number of casual users
  `registered`   Number of registered users
  `cnt`          Total bike rentals

The target is:

``` text
cnt = casual + registered
```
------------------------------------------------------------------------

## Analysis Workflow

``` text
Data Loading
     ↓
Data Understanding
     ↓
Exploratory Data Analysis
     ├── Numerical Analysis
     ├── Categorical Analysis
     └── Relationship with Target
     ↓
Data Preparation
     ├── Remove irrelevant variables
     ├── Convert categorical variables
     └── Create dummy variables
     ↓
Train-Test Split
     ↓
Feature Selection
     ├── Correlation Analysis
     ├── VIF Analysis
     └── Statistical Significance
     ↓
Multiple Linear Regression
     ↓
Model Evaluation
     ├── R²
     └── Predictions
     ↓
Residual Analysis
     ├── Normality
     ├── Linearity
     └── Homoscedasticity
     ↓
Final Model Interpretation
```

------------------------------------------------------------------------

## Exploratory Data Analysis

### Categorical Analysis

Season, weather situation, holiday, month, weekday, working day, and
year were compared against total bike rentals.

Key observations from the original analysis included:

-   Spring had the lowest rental counts, while fall had the highest.
-   Clear or partly cloudy weather was associated with higher demand.
-   Heavy rain or snow was associated with very low demand.
-   September showed particularly high rental demand, while January
    showed relatively low demand.
-   Working days generally showed higher demand than non-working days.
-   Median rental demand increased from 2018 to 2019.

### Numerical Analysis

Temperature, feeling temperature, humidity, wind speed, casual users,
and registered users were examined using distributions, scatter plots,
pair plots, and correlation analysis.

The original analysis reported the following correlations with `cnt`:

  Variable         Correlation with `cnt`
  -------------- ------------------------
  `registered`                       0.95
  `casual`                           0.67
  `temp`                             0.63
  `atemp`                            0.63

The very strong relationship with `registered` and `casual` is expected
because these variables directly contribute to the target:

``` text
cnt = casual + registered
```

These variables require careful consideration when
interpreting a predictive model.

------------------------------------------------------------------------

## Data Preparation

### Categorical Encoding

Variables such as `season`, `mnth`, `weekday`, `weathersit`, and `yr`
were treated as categorical variables where appropriate and converted
into dummy variables.

`drop_first=True` was used during dummy-variable creation to establish a
reference category and reduce redundant information that can introduce
multicollinearity.

### Feature Selection

Feature selection considered:

-   Correlation with the target
-   Correlation among predictors
-   Statistical significance
-   Variance Inflation Factor (VIF)

This helped reduce redundant predictors and improve model stability and
interpretability.

------------------------------------------------------------------------

## Model Building

A **Multiple Linear Regression** model was developed using the prepared
independent variables.

The model estimates daily bike demand as:

``` text
cnt = β₀ + β₁X₁ + β₂X₂ + ... + βₙXₙ
```

The model was trained on a training subset and evaluated on a separate
test set.

Both `statsmodels` and `scikit-learn` were used:

-   **Statsmodels** for statistical interpretation and significance
    analysis.
-   **Scikit-learn** for train-test splitting and test-set evaluation.

------------------------------------------------------------------------

## Model Evaluation

The model was evaluated using **R² (R-squared)**.

R² measures the proportion of variation in the target variable explained
by the model.

The assignment specifically required calculating the R² score on the
test dataset. The notebook contains the complete prediction and
evaluation workflow.

------------------------------------------------------------------------

## Multicollinearity Analysis

Multicollinearity was examined using correlation heatmaps and Variance
Inflation Factor (VIF).

Predictors with high VIF values were investigated and the feature set
was refined to improve model stability and interpretability.

------------------------------------------------------------------------

## Residual Analysis

Residual analysis was performed after model building to assess whether
the regression model satisfied important assumptions.

The analysis examined:

-   Distribution of residuals
-   Residual patterns
-   Normality of residuals
-   Relationship between predicted values and residuals
-   Homoscedasticity

The original analysis found the residual distribution to be
approximately normal with a mean near zero.

------------------------------------------------------------------------

## Linear Regression Assumptions

### Linearity

The relationship between predictors and the target should be
approximately linear. Scatter plots and model diagnostics were used to
examine this assumption.

### Multicollinearity

Predictors should not have excessive linear dependence on one another.
Correlation analysis and VIF were used for this purpose.

### Normality of Residuals

Residuals should approximately follow a normal distribution. A residual
distribution and Q-Q plot were used to assess this assumption.

### Homoscedasticity

Residual variance should remain reasonably consistent across predicted
values. Residual plots were used to investigate this assumption.

------------------------------------------------------------------------

## Key Findings

### Temperature

Temperature was one of the strongest predictors in the final model and
had a positive relationship with bike demand.

### Weather Situation

Poor weather conditions were associated with lower bike demand. The
`weathersit_3` category, representing conditions such as light snow,
light rain, thunderstorms, and scattered clouds, had a negative
coefficient relative to the reference weather category.

### Year

The year variable was retained because bike-sharing demand increased
over time. The analysis indicated higher demand in the later year of the
dataset.

### Season and Working Patterns

Seasonal and working-day effects also contributed to differences in
daily demand.

Overall, the analysis showed that weather, temperature, seasonality,
time, and working patterns can provide useful information for
understanding shared-bike demand.

------------------------------------------------------------------------

## Top Predictors in the Final Model

Based on the original final-model interpretation, three of the most
significant predictors were:

1.  **Temperature (`temp`)** --- positive contribution to demand.
2.  **Weather situation (`weathersit_3`)** --- negative contribution
    relative to the reference weather category.
3.  **Year (`yr`)** --- positive contribution associated with increased
    demand over time.

The exact coefficient values and statistical outputs are available in
the original notebook.

------------------------------------------------------------------------

## Technologies & Libraries

-   Python
-   Pandas
-   NumPy
-   Matplotlib
-   Seaborn
-   Statsmodels
-   Scikit-learn
-   Jupyter Notebook / Google Colab

------------------------------------------------------------------------

## Project Files

### `Linear_Regression_Assignment_Final.ipynb`

The main Jupyter Notebook containing:

-   Data loading and understanding
-   Exploratory data analysis
-   Data preparation
-   Categorical encoding
-   Feature selection
-   Correlation analysis
-   VIF analysis
-   Train-test split
-   Multiple linear regression
-   Model evaluation
-   Residual analysis
-   Assumption checking
-   Final model interpretation

### `Linear Regression Assignment Questions.pdf`

The completed subjective-question component covering:

-   Linear regression
-   Anscombe's quartet
-   Pearson correlation
-   Feature scaling
-   Regression assumptions
-   VIF and multicollinearity
-   Q-Q plots
-   Interpretation of the final model

------------------------------------------------------------------------

## Limitations

This project is an **academic regression case study**.

The model uses historical daily observations and a limited feature set.
Real-world demand forecasting would typically incorporate additional
information such as location-level demand, pricing, availability,
events, traffic, holidays, weather forecasts, and operational factors.

------------------------------------------------------------------------

## Learning Outcomes

This project provided practical experience with:

-   Exploratory data analysis
-   Regression problem formulation
-   Categorical variable encoding
-   Feature selection
-   Multiple linear regression
-   Train-test splitting
-   Model evaluation using R²
-   Statistical interpretation using Statsmodels
-   Multicollinearity analysis using VIF
-   Residual diagnostics
-   Regression assumption validation
-   Interpreting model coefficients
-   Translating model results into business insights

------------------------------------------------------------------------

## Project Context

This project was completed as part of an academic machine-learning
assignment focused on predicting shared-bike demand using multiple
linear regression.

It demonstrates the workflow of developing and interpreting an
interpretable regression model, from exploratory analysis and feature
preparation through model diagnostics and evaluation.

