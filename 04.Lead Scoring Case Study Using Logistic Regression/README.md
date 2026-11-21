# Lead Scoring Case Study Using Logistic Regression

## Overview

This project is an academic machine learning case study focused on
**lead scoring and lead conversion prediction**. The objective is to
help an education company identify the leads that are most likely to
convert into paying customers so that the sales team can prioritize its
efforts.

The project uses historical lead data and builds a **logistic regression
model** to estimate the probability of lead conversion. These
probabilities are then converted into a **lead score from 0 to 100**,
where a higher score represents a higher estimated likelihood of
conversion.

The project covers data cleaning, exploratory data analysis, feature
preparation, feature selection, logistic regression model building,
statistical evaluation, probability threshold selection, and business
recommendations.

## Problem Statement

X Education generates a large number of leads but has a relatively low
lead conversion rate of around 30%. The company wants to identify its
most promising leads, or **Hot Leads**, so that the sales team can focus
more attention on leads with a higher probability of conversion.

The business has set a target conversion rate of approximately 80% for
the leads identified as potential converters. The case study therefore
requires a model that assigns each lead a score between 0 and 100, with
higher scores indicating a higher likelihood of conversion. The problem
statement specifies that the historical dataset contains around 9,000
lead records and includes variables such as Lead Source, Total Time
Spent on Website, Total Visits, Last Activity, and others. The target
variable is `Converted`, where `1` represents a converted lead and `0`
represents a lead that was not converted. 

## Objectives

-   Understand the factors associated with lead conversion.
-   Clean and prepare the historical lead dataset.
-   Perform exploratory data analysis to identify useful patterns.
-   Build a logistic regression model for binary lead-conversion
    prediction.
-   Select a meaningful set of predictors using RFE, statistical
    significance, and VIF.
-   Evaluate the model using accuracy, sensitivity, specificity,
    precision, recall, and ROC-AUC.
-   Determine a probability cutoff for classifying leads as converted or
    not converted.
-   Convert predicted probabilities into lead scores from 0 to 100.
-   Translate model findings into practical sales and lead-nurturing
    recommendations.

The assignment specifically requires a logistic regression model that
assigns a lead score between 0 and 100 and a presentation explaining the
technical and business results. 

## Dataset

The project uses a historical lead dataset referred to as `Leads.csv`.

The notebook shows the following dataset progression:

  -----------------------------------------------------------------------
  Stage                                                             Shape
  ------------------------------ ----------------------------------------
  Original dataset                                             9,240 × 37

  After removing columns with                                  9,240 × 30
  more than 40% missing values   

  After additional cleaning and                                9,240 × 27
  dropping identifier columns    

  After univariate analysis and                                9,240 × 12
  removal of low-value variables 

  After dummy-variable encoding                                9,240 × 81

  Training set                                                 6,468 × 80

  Test set                                                     2,772 × 80
  -----------------------------------------------------------------------

The target variable is `Converted`.

-   `0` = lead was not converted
-   `1` = lead was converted

The overall conversion rate in the cleaned dataset was approximately
**38.54%**.

The original problem statement describes the dataset as containing
around 9,000 historical leads and explicitly identifies `Converted` as
the target variable.

## Data Cleaning

The notebook performs several stages of data cleaning and preparation.

### Handling `Select` Values

Several categorical columns contain the value `Select`. The project
treats this value as equivalent to a missing response and replaces it
with `NaN` before performing missing-value analysis. This follows the
assignment's instruction that `Select` should be handled as a null-like
value. 

### Removing High-Missing-Value Columns

Columns with more than 40% missing values were removed. The notebook
specifically identifies variables such as:

-   `Asymmetrique Activity Index`
-   `Asymmetrique Profile Index`
-   `Asymmetrique Activity Score`
-   `Asymmetrique Profile Score`
-   `How did you hear about X Education`
-   `Lead Profile`
-   `Lead Quality`

as having high levels of missing data and being unsuitable for the
analysis.

### Missing-Value Treatment

Selected remaining variables were imputed using approaches appropriate
to their type and context, including:

-   `Specialization` → `Other`
-   `Lead Source` → standardized and missing values filled with `Google`
-   `TotalVisits` → median
-   `Page Views Per Visit` → median
-   `Last Activity` → `Email Opened`
-   `What is your current occupation` → `Other`
-   `What matters most to you in choosing a course` →
    `Better Career Prospects` before the variable was later removed
-   `Country` → `India`
-   `City` → `Mumbai`
-   `Tags` → `Will revert after reading the email`

The notebook also groups several low-frequency categorical values into
broader `Other`/`Others` categories.

### Identifier Removal

`Prospect ID` and `Lead Number` were removed because they function as
identifiers rather than predictive features.

## Exploratory Data Analysis

EDA was used to understand the distribution of variables and identify
relationships with lead conversion.

The target analysis showed a conversion rate of approximately **38.54%**
in the cleaned dataset.

The project examines categorical variables such as:

-   Lead Origin
-   Lead Source
-   Last Activity
-   Tags
-   Specialization
-   Current Occupation
-   City
-   Last Notable Activity

Numerical analysis focused particularly on:

-   `TotalVisits`
-   `Total Time Spent on Website`
-   `Page Views Per Visit`

The pairplot in the presentation shows that higher values of website
visits, page views per visit, and time spent on the website were
associated with a higher proportion of converted leads. The correlation
analysis reports a correlation of **0.36** between
`Total Time Spent on Website` and `Converted`, while `TotalVisits` and
`Page Views Per Visit` have a relatively high correlation of **0.77**
with each other.

## Feature Engineering and Data Preparation

Categorical variables were converted into dummy variables using one-hot
encoding with `drop_first=True`.

Dummy variables were created for:

-   Lead Origin
-   Lead Source
-   Last Activity
-   Tags
-   Specialization
-   Current Occupation
-   City
-   Last Notable Activity

The three main numerical variables were standardized using
`StandardScaler`:

-   `TotalVisits`
-   `Total Time Spent on Website`
-   `Page Views Per Visit`

The data was split into training and test sets using a **70:30 ratio**
with `random_state=100`.

## Feature Selection

The project uses a combination of automated feature selection and
statistical model refinement.

### Recursive Feature Elimination

RFE was initially used with a logistic regression estimator to select
**20 features** from the prepared dataset.

The selected variables were then evaluated using a sequence of
Generalized Linear Models with a binomial family and logit link.

### Iterative Model Refinement

Nine model iterations were developed. Variables with relatively high
p-values were removed progressively, followed by VIF-based checks for
multicollinearity.

Variables removed during the iterative process included:

-   `Tags_wrong number given`
-   `Tags_Not doing further education`
-   `Lead Source_Facebook`
-   `Tags_invalid number`
-   `Last Notable Activity_Had a Phone Conversation`
-   `Last Notable Activity_Email Link Clicked`
-   `Tags_switched off`
-   `Last Notable Activity_Olark Chat Conversation`

The final Model 9 contained **12 predictor variables plus the
constant**. The notebook reports low VIF values for the final variables,
with the highest VIF being approximately 3.33.

## Final Logistic Regression Model

The final model was built using `statsmodels` GLM with:

-   **Family:** Binomial
-   **Link function:** Logit
-   **Training observations:** 6,468
-   **Predictors:** 12
-   **Pseudo R-squared (CS):** approximately 0.6105

The final model variables were:

  Variable                                                   Coefficient
  -------------------------------------------------------- -------------
  `Total Time Spent on Website`                                   0.9371
  `Lead Origin_Lead Add Form`                                     1.6948
  `Last Activity_Email Bounced`                                  -1.8118
  `Last Activity_SMS Sent`                                        1.9729
  `Tags_Busy`                                                     2.6362
  `Tags_Closed by Horizzon`                                       9.2047
  `Tags_Lost to EINS`                                            10.9851
  `Tags_Ringing`                                                 -1.1699
  `Tags_Will revert after reading the email`                      5.3743
  `What is your current occupation_Other`                        -3.7292
  `What is your current occupation_Working Professional`          1.2544
  `Last Notable Activity_Modified`                               -1.3787

The final model equation is documented in the project summary and
subjective-question file. The three largest positive coefficients are
`Tags_Lost to EINS`, `Tags_Closed by Horizzon`, and
`Tags_Will revert after reading the email`.

## Model Evaluation

The project evaluates the model using multiple classification metrics
rather than accuracy alone.

### Training Performance

Using the initial 0.50 probability cutoff, the training confusion matrix
was:

``` text
[[3805, 197],
 [ 263, 2203]]
```

The corresponding metrics were:

  Metric                        Result
  --------------------------- --------
  Accuracy                      92.89%
  Sensitivity / Recall          89.33%
  Specificity                   93.50%
  Precision / PPV               91.79%
  Negative Predictive Value     94.61%

The presentation reports these evaluation results and explains
sensitivity as the ability to identify converted leads and specificity
as the ability to identify leads that are unlikely to convert.

### ROC-AUC

The ROC analysis produced an **AUC of approximately 0.97** in the
project analysis, indicating strong separation between converted and
non-converted leads within the evaluated data.

### Probability Cutoff

Instead of relying permanently on the arbitrary 0.50 cutoff, the project
evaluated multiple probability thresholds and selected **0.38** as the
optimal cutoff based on the balance between accuracy, sensitivity, and
specificity on the training data.

This cutoff was then used to create the final lead classification and
lead score:

``` text
Lead Score = Predicted Conversion Probability × 100
```

For example, a predicted probability of `0.84` corresponds to a lead
score of approximately `84`.

The lead score therefore provides a continuous ranking mechanism, while
the cutoff converts probabilities into binary classifications.

## Test-Set Evaluation

The final model was applied to the held-out test set.

The project reports the following test-set results using the final
classification procedure documented in the notebook/presentation:

  Metric                   Test Result
  ---------------------- -------------
  Accuracy                      91.85%
  Sensitivity / Recall          96.07%
  Specificity                   89.09%

The test confusion matrix in the notebook is:

``` text
[[1494, 183],
 [  43, 1052]]
```

The project therefore demonstrates reasonably consistent performance
between the training and test sets, with particularly high test
sensitivity.

## Lead Scoring

The core business output of the project is a **0--100 lead score**.

The model first produces a conversion probability for each lead. This
probability is then multiplied by 100 and rounded to create the lead
score.

Conceptually:

``` text
Higher probability → Higher Lead Score → Hotter Lead
Lower probability  → Lower Lead Score  → Colder Lead
```

This allows the sales team to rank leads and prioritize outreach instead
of treating every lead equally.

## Key Findings

The final model and EDA identify several variables associated with lead
conversion:

1.  **Tags-related variables** are among the strongest model predictors,
    particularly `Tags_Lost to EINS`, `Tags_Closed by Horizzon`, and
    `Tags_Will revert after reading the email`.
2.  **Total Time Spent on Website** has a positive coefficient,
    indicating that greater website engagement is associated with a
    higher estimated conversion probability in the model.
3.  **SMS-based activity** is positively associated with conversion.
4.  **Lead Origin -- Lead Add Form** has a positive coefficient in the
    final model.
5.  **Working Professional** is positively associated with conversion
    relative to the model's reference category.
6.  Some activity states, including `Email Bounced`, `Ringing`, and
    `Last Notable Activity_Modified`, have negative coefficients.

The assignment's subjective analysis similarly identifies the three
largest positive model coefficients as `Tags_Lost to EINS`,
`Tags_Closed by Horizzon`, and
`Tags_Will revert after reading the email`.

## Business Recommendations

The project translates the model and EDA findings into sales strategies.

### During High-Activity Periods

When the company has additional sales capacity, the analysis recommends
prioritizing leads with characteristics associated with higher
conversion probability, including:

-   Working professionals
-   Leads showing higher website engagement
-   Leads with `Last Activity` indicating SMS sent or email engagement
-   Leads with promising Tags
-   Leads from higher-converting specializations, particularly
    management-related areas

The assignment also suggests increasing phone outreach and using
incentives such as discounts or free trials during periods when the
company wants to maximize conversions.

### During Low-Activity / Target-Achieved Periods

When the sales team has already reached its quarterly target, the
project recommends reducing unnecessary calls and focusing effort on
higher-scoring leads.

Lower-scoring leads can instead be placed into targeted email or SMS
nurturing campaigns until they become more sales-ready. The analysis
also recommends respecting communication preferences such as
`Do Not Email`. 

## Visualizations

The project includes visual analysis covering:

-   Missing-value distributions
-   Categorical variable distributions
-   Univariate analysis
-   Pairplots
-   Correlation heatmaps
-   Model evaluation curves
-   ROC curve
-   Accuracy, sensitivity, and specificity across probability cutoffs
-   Precision-recall analysis
-   Confusion matrices

The presentation contains 23 slides covering the problem statement,
data, workflow, cleaning, EDA, feature preparation, model building,
evaluation, predictions, conclusions, and recommendations.


## Technologies & Libraries

### Programming Language

-   Python

### Libraries

-   Pandas
-   NumPy
-   Matplotlib
-   Seaborn
-   Scikit-learn
-   Statsmodels

### Techniques

-   Data cleaning
-   Missing-value treatment
-   Exploratory data analysis
-   One-hot encoding
-   Standardization
-   Train-test splitting
-   Logistic regression
-   Generalized Linear Models
-   Recursive Feature Elimination (RFE)
-   Variance Inflation Factor (VIF)
-   Probability threshold optimization
-   Confusion matrix analysis
-   ROC-AUC
-   Precision and recall
-   Lead scoring


### File Descriptions

**`Lead_Scoring_Case_Study.ipynb`**\
Main analysis notebook containing data cleaning, EDA, feature
preparation, RFE, logistic regression model development, model
evaluation, lead scoring, and test-set predictions.

**`Assignment Subjective Questions.pdf`**\
Business-oriented questions and the corresponding recommendations based
on the model and EDA.

**`Presentation.pdf`**\
Presentation of the technical approach, model results, visualizations,
findings, and business recommendations.

**`Summary.pdf`**\
Brief summary of the approach, modeling process, results, and learning
outcomes.

## Limitations

This project is an **academic case study**.

A few points are important when interpreting the original
analysis:

-   The model is based on historical lead behavior and should not
    automatically be interpreted as causal evidence that changing a
    particular variable will cause conversion.
-   The 80% conversion rate is the company's target described in the
    case study; the model's reported accuracy or lead score does not
    itself establish that the company will achieve an 80% real-world
    conversion rate.
-   The notebook contains a specific probability-threshold workflow: it
    selects 0.38 for the training analysis, while the later test-set
    prediction code uses a 0.25 cutoff. 
-   The notebook applies `fit_transform` separately to the test-set
    numerical features rather than reusing the scaler fitted on the
    training data. 
-   The reported evaluation metrics should therefore be understood as
    results of the original academic notebook rather than as a
    production validation benchmark.

## Learning Outcomes

This project demonstrates practical understanding of:

-   Business problem formulation for binary classification
-   Data cleaning and missing-value treatment
-   Exploratory data analysis
-   Handling categorical variables
-   One-hot encoding
-   Feature scaling
-   Train-test splitting
-   Logistic regression
-   Statistical model interpretation
-   Recursive Feature Elimination
-   Multicollinearity analysis using VIF
-   Model evaluation using classification metrics
-   ROC-AUC analysis
-   Probability threshold selection
-   Probability-based lead scoring
-   Translating model output into business recommendations

## Project Context

This project was completed as an academic case study and is included in
the **Academic Projects** collection to demonstrate foundational machine
learning, statistical modeling, EDA, and business-analysis skills.


