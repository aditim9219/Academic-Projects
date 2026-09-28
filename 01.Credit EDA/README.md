# Credit Risk Exploratory Data Analysis

## Overview

This project is an academic Exploratory Data Analysis (EDA) case study based on the consumer lending and credit-risk domain.

The objective of the analysis was to explore patterns associated with clients experiencing payment difficulties and identify the customer and loan attributes that appear to differentiate defaulters from clients who repay their loans.

The analysis uses application-level information together with previous loan application history and covers data cleaning, missing-value analysis, outlier analysis, data imbalance, categorical and numerical analysis, correlation analysis, and analysis of the merged datasets.

> **Project Type:** Academic / Exploratory Data Analysis  
> **Domain:** Banking & Financial Services / Credit Risk  
> **Tools:** Python, Pandas, NumPy, Matplotlib, Seaborn, Jupyter Notebook

---

## Problem Statement

Loan providers face a difficult balance when assessing loan applications:

- Approving a loan for an applicant who is likely to default can result in financial losses.
- Rejecting an applicant who is capable of repaying the loan can result in lost business opportunities.

The purpose of this case study was to use exploratory data analysis to understand patterns associated with loan repayment difficulties and identify variables that may be useful for assessing credit risk.

The target variable represents whether a client experienced payment difficulties:

- `TARGET = 0` — Repayer / client without payment difficulties
- `TARGET = 1` — Defaulter / client with payment difficulties

---

## Objectives

The main objectives of the analysis were to:

1. Understand the structure and characteristics of the application datasets.
2. Identify and handle missing values.
3. Identify and examine potential outliers.
4. Analyze the imbalance in the target variable.
5. Perform categorical univariate and segmented analysis.
6. Perform categorical bivariate and multivariate analysis.
7. Analyze numerical variables and their distributions.
8. Compare numerical relationships between repayers and defaulters.
9. Identify important correlations within the two target segments.
10. Merge current application information with previous application history.
11. Extract business-oriented insights from the exploratory analysis.

---

## Dataset

The original case study used three files:

| Dataset | Description |
|---|---|
| `application_data.csv` | Information about clients at the time of their current loan application |
| `previous_application.csv` | Information about the client's previous loan applications |
| `columns_description.csv` | Data dictionary describing the variables |

The original `application_data.csv` contained **307,511 rows and 122 columns**.

The `previous_application.csv` dataset contained **1,670,214 rows and 37 columns**.

The two main datasets were eventually combined using the client identifier `SK_ID_CURR` for analysis of current and previous application behaviour.

The notebook and presentation represent the original academic analysis performed using the dataset.

---

## Analysis Workflow

The analysis followed the following overall workflow:

```text
Data Loading
     │
     ▼
Data Understanding
     │
     ▼
Missing-Value Analysis
     │
     ▼
Data Cleaning
     │
     ├── Remove / retain high-null columns
     ├── Handle missing values
     ├── Standardize values
     └── Convert appropriate datatypes
     │
     ▼
Outlier Analysis
     │
     ▼
Target / Data Imbalance Analysis
     │
     ▼
Categorical Analysis
     │
     ├── Univariate Analysis
     ├── Segmented Univariate Analysis
     └── Bivariate / Multivariate Analysis
     │
     ▼
Numerical Analysis
     │
     ├── Correlation Analysis
     ├── Distribution Analysis
     └── Bivariate Analysis
     │
     ▼
Merge Current + Previous Applications
     │
     ▼
Merged Dataset Analysis
     │
     ▼
Business Insights & Conclusions

```
---

## Data Cleaning
### Application Dataset

The application dataset initially contained a large number of variables with missing values.

The cleaning process included:

1. Calculating the percentage of missing values for each variable.
2. Identifying variables with very high proportions of missing data.
3. Removing variables with excessive missing values where appropriate.
4. Investigating variables with moderate levels of missing data.
5. Examining variables individually before deciding how missing values should be handled.
6. Removing variables considered irrelevant to the analysis.
7. Standardizing selected variables.
8. Converting appropriate columns to categorical datatypes.

Variables with more than 50% missing values were initially identified and removed.

Additional variables with substantial missing values were evaluated individually rather than applying a single imputation strategy to every column.

### Missing-Value Treatment

Different approaches were used depending on the characteristics of the variable:

1. Categorical variables such as `OCCUPATION_TYPE` and `NAME_TYPE_SUITE` were assigned an Unknown category where appropriate.
2. Selected numerical variables were imputed using their median values.
3. Rows with missing `AMT_GOODS_PRICE` values were removed after examining the distribution of the variable.
4. Other unnecessary variables were removed during the cleaning process.

---

## Outlier Analysis

Boxplots and descriptive statistics were used to identify potential outliers in numerical variables.

Outliers were examined in variables such as:

* `AMT_CREDIT`
* `AMT_ANNUITY`
* `AMT_APPLICATION`
* `AMT_GOODS_PRICE`
* `SELLERPLACE_AREA`
* `CNT_PAYMENT`
* Other numerical application attributes

The analysis considered the context of the variables before deciding whether extreme observations should be removed or retained.

In particular, some extreme financial values could represent legitimate high-value loans or applicants rather than erroneous observations.

---

## Target Variable & Data Imbalance

The target variable was analyzed to understand the distribution between:

* `Repayers (TARGET = 0)`
* `Defaulters (TARGET = 1)`

Because the target classes are imbalanced, both absolute counts and relative/default percentages were considered during the analysis.

This was important when interpreting categorical and numerical relationships because a variable could have a large number of observations in one category without necessarily having a proportionally high default rate.

---

## Exploratory Data Analysis
### Categorical Analysis

Categorical variables were analyzed using segmented univariate analysis to compare repayers and defaulters.

Variables explored included attributes such as:

* Contract type
* Gender
* Family status
* Education type
* Income type
* Occupation type
* Organization type
* Housing type
* Number of children
* Number of family members
* Property ownership
* Other application attributes

The analysis compared both the distribution of applicants and the corresponding default rates.

### Categorical Bivariate / Multivariate Analysis

Relationships between categorical and numerical variables were also explored.

For example, income-related variables were examined across income categories and repayment status to understand how financial characteristics differed between groups.

---

## Numerical Analysis

Numerical variables were analyzed using:

* Descriptive statistics
* Distribution plots
* Correlation matrices
* Heatmaps
* Scatter plots
* Pair plots
* Segmented analysis based on TARGET

Important financial variables included:

* `AMT_INCOME_TOTAL`
* `AMT_CREDIT`
* `AMT_ANNUITY`
* `AMT_GOODS_PRICE`

---

## Correlation Analysis

The application dataset was segmented into two groups:

`Repayers  → TARGET = 0`
`Defaulters → TARGET = 1`

Correlation matrices were then generated separately for the two groups.

The analysis focused on identifying the strongest relationships among numerical variables rather than treating the target variable as a continuous correlation variable.

Among the observed relationships:

* `AMT_CREDIT` showed a strong relationship with `AMT_GOODS_PRICE`.
* `AMT_CREDIT` and `AMT_ANNUITY` were also strongly related.
* The relationship between total income and credit amount differed between the repayer and defaulter segments.

The analysis also highlighted that individual numerical variables did not provide complete separation between repayers and defaulters because their distributions showed considerable overlap.

---

## Previous Application Analysis

The `previous_application.csv` dataset was independently cleaned and analyzed before being combined with the current application data.

Previous application attributes included information about previous loan decisions such as:

* Approved
* Cancelled
* Refused
* Unused offer

The analysis examined how previous application outcomes related to the repayment behaviour represented by the current TARGET variable.

---

## Merged Dataset Analysis

The cleaned application dataset and previous application dataset were merged using:

* `SK_ID_CURR`

The merged dataset enabled analysis of current repayment behaviour together with previous application history.

The analysis examined relationships involving:

* Previous contract status
* Loan purpose
* Current repayment status
* Previous application outcomes
* Applicant financial characteristics

One of the observations from the analysis was that a substantial proportion of previously refused applicants in the analyzed sample subsequently appeared as repayers in their current application.

This highlighted the importance of considering previous application history carefully rather than treating a previous rejection as a definitive indicator of future repayment behaviour.

---

## Key Findings

The exploratory analysis identified several patterns in the dataset.

### Applicant Characteristics

Differences in default rates were observed across several categorical attributes, including:

* Contract type
* Gender
* Education
* Income type
* Occupation
* Family status
* Housing-related attributes

The analysis also showed that applicant population size and default rate do not necessarily move together. Some categories contained many applicants but had relatively moderate default rates, while smaller categories sometimes showed higher default percentages.

### Financial Variables

The analysis found strong relationships among several loan-related variables.

In particular:

```text
AMT_CREDIT
      ↕
AMT_GOODS_PRICE

AMT_CREDIT
      ↕
AMT_ANNUITY

```

The distributions of income, credit amount, annuity amount, and goods price also showed substantial overlap between repayers and defaulters.

Therefore, these variables should not be interpreted individually as definitive indicators of repayment behaviour.

### Previous Applications

Previous application status provided additional context for understanding current repayment behaviour.

The merged analysis demonstrated the value of combining current application information with historical application information rather than analyzing the current application in isolation.

---

## Visualizations

The project contains a variety of visualizations, including:

* Count plots
* Bar plots
* Box plots
* Distribution plots
* KDE plots
* Heatmaps
* Scatter plots
* Pair plots
* Segmented categorical visualizations

These visualizations were used to investigate distributions, missing values, outliers, class imbalance, relationships between variables, and differences between repayers and defaulters.

---

## Technologies & Libraries
### Programming Language
* Python

### Libraries
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Itertools

### Environment
* Jupyter Notebook

---

## Project Files
### Credit_EDA_Assignment.ipynb

The main Jupyter Notebook containing:

* Data loading
* Data cleaning
* Missing-value handling
* Outlier analysis
* Data standardization
* Exploratory analysis
* Correlation analysis
* Merged dataset analysis
* Visualizations
* Findings and conclusions

### Credit-EDA-Case-Study.pdf

The presentation created to summarize the analysis, methodology, visualizations, findings, and conclusions.

---

## Limitations

This project is an exploratory data analysis study and does not develop or evaluate a machine-learning model for loan default prediction.

The findings represent patterns observed in the dataset and should not be interpreted as causal relationships.

Additionally, the original dataset is no longer available in this repository, so the notebook cannot currently be executed end-to-end without obtaining the original data files.

---

## Learning Outcomes

This project provided practical experience with:

* Working with large tabular datasets
* Understanding a financial-services business problem
* Data-quality assessment
* Missing-value analysis and treatment
* Outlier investigation
* Handling imbalanced target variables
* Categorical and numerical EDA
* Segmented analysis
* Correlation analysis
* Data visualization using Python
* Combining current and historical application data

---

## Project Context

This project was completed as part of an academic EDA case study focused on applying exploratory data analysis techniques to a real-world-style banking and financial-services problem.

It demonstrates the application of fundamental data-analysis techniques rather than a novel research contribution or production credit-risk system.

Translating analytical observations into business-oriented insights
