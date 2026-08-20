# Predicting Future High-Value Physician-Industry Relationships Among Nephrologists Using CMS Open Payments Data

**Author:** Colleen Yap  
**Program:** Professional Certificate in Machine Learning \& Artificial
Intelligence

## Executive Summary

The objective of this project is to determine whether historical CMS
Open Payments activity can be used to identify and rank nephrology
recipients who are more likely to become high-value payment recipients
in the following year.

Using publicly available CMS Open Payments General Payments data,
historical features were developed from 2020-2023 payment activity and
used to predict high-value recipient status in 2024. Four classification
algorithms were evaluated: Logistic Regression, Decision Tree, Random
Forest, and Gradient Boosting. Gradient Boosting was subsequently
optimized using five-fold cross-validation and Grid Search, followed by
classification-threshold selection using cross-validated training
predictions.

The final tuned Gradient Boosting model used a **0.30 classification
threshold** and achieved **92.82% accuracy, 66.67% precision, 69.82%
recall, an F1-score of 0.6821, and a ROC-AUC of 0.8933** on the
independent test set. The model correctly identified **118 of 169 actual
high-value recipients**.

<img width="429" height="686" alt="image" src="https://github.com/user-attachments/assets/fa3ad5bf-e990-4a33-9ec6-bf691c4caa1c" />

The final model is intended as a **ranking and prioritization tool**
that complements professional judgment and other relevant organizational
information rather than serving as a standalone decision-making tool.

## Business Problem

CMS Open Payments provides transparency into financial relationships
between life sciences companies and covered healthcare recipients,
including physicians and certain other healthcare professionals such as
nurse practitioners. The data are primarily retrospective and describe
payment activity that has already occurred.

This project evaluates whether historical payment and
industry-engagement patterns can provide an additional data-driven
signal for identifying nephrology recipients who are more likely to
become high value in a subsequent year. When engagement resources are
limited, model-generated rankings may help focus further review on
recipients with stronger predictive signals.

## Research Question

**Can historical CMS Open Payments patterns from 2020--2023 be used to
predict and rank nephrology recipients according to their likelihood of
becoming high-value payment recipients in 2024?**

For the 2024 outcome, recipients with total General Payments meeting or
exceeding the study's high-value threshold of **$2,054.10** were
classified as high value. In the final modeling dataset, **845 of 7,664
recipients (11.03%)** were classified as high value and **6,819
(88.97%)** as non-high value.

<img width="884" height="153" alt="HighValueVsNonHighValue" src="https://github.com/user-attachments/assets/638ac671-ad72-4999-98bf-da860b23c143" />


## Data Source

The project uses publicly available **CMS Open Payments General
Payments** data from 2020 through 2024.

* Source: [CMS Open Payments](https://openpaymentsdata.cms.gov/)
* Historical predictor period: **2020--2023**
* Prediction outcome: **2024 high-value status**
* Specialty: **Nephrology**

## Data Engineering

A SQL Server data pipeline was used to clean, integrate, aggregate, and
engineer the modeling data.

The historical 2020--2023 table contained **10,532 recipients**, while
the separately created 2024 target table contained approximately **8,698
recipients**. An **INNER JOIN** combined the two tables, keeping
historical recipients with matching 2024 records. After the
inner join and modeling criteria were applied, the final dataset
contained **7,664 recipients**.

Historical predictors included payment amounts, payment frequency, years
of activity, payment categories, and measures of the breadth and
diversity of industry relationships.

<img width="1909" height="1126" alt="image" src="https://github.com/user-attachments/assets/1e56f1dc-265f-42a3-a6dc-8d87ad74ebcd" />

## Exploratory Data Analysis

EDA examined:

* Dataset structure, data types, missing values, and duplicate records
* Target class distribution
* Historical payment distributions and skewness
* Consulting, speaker or honoraria, travel and lodging, and food and
beverage payments
* Recipient primary type and geographic distribution
* Active years and payment-frequency patterns
* High-value versus non-high-value recipient characteristics
* Correlations between historical features and 2024 high-value status

Correlation analysis showed that payment-type diversity and payment frequency had the strongest relationships with future high-value status. Food and beverage activity and speaker or honoraria payments also showed positive associations with the outcome. In contrast, payment-amount variables showed relatively weak individual linear correlations with future high-value status, although some of these features contributed to the final Gradient Boosting model when considered alongside other predictors.

<img width="694" height="682" alt="CorrelationTo2024" src="https://github.com/user-attachments/assets/44c89ce6-fd06-449b-9cfb-bbf3e74c1c80" />


## Machine Learning Methodology

Four classification algorithms were developed and compared:

* Logistic Regression
* Decision Tree
* Random Forest
* Gradient Boosting

The workflow also included:

* Stratified train/test splitting
* One-hot encoding of categorical variables
* Standardization of numerical features where appropriate
* Five-fold stratified cross-validation
* Grid Search hyperparameter tuning for Gradient Boosting
* Cross-validated classification-threshold selection
* Feature-importance analysis
* Ranking and business-prioritization validation

Grid Search identified the following Gradient Boosting hyperparameters:

* `learning\_rate = 0.05`
* `max\_depth = 2`
* `min\_samples\_leaf = 5`
* `n\_estimators = 200`

The best cross-validated ROC-AUC was **0.9178**. Cross-validated
training predictions were then used to evaluate alternative
classification thresholds, and **0.30** was selected because it provided
the strongest F1-score while maintaining relatively high recall.

<img width="411" height="230" alt="image" src="https://github.com/user-attachments/assets/31952191-3041-43f2-a5d6-46e3c9ec36ab" />



## Model Performance

\---

Model            Accuracy    Precision       Recall     F1 Score      ROC-AUC

\---

Tuned              0.9282       0.6667       0.6982   **0.6821**   **0.8933**
Gradient  
Boosting  
(0.30)

Gradient           0.9022       0.5404   **0.7515**       0.6287       0.8920
Boosting

Random         **0.9341**       0.7742       0.5680       0.6553       0.8851
Forest

Logistic           0.9276   **0.7959**       0.4615       0.5843       0.8621
Regression

Decision           0.9002       0.5465       0.5562       0.5513       0.7495
Tree
---
<img width="1347" height="786" alt="image" src="https://github.com/user-attachments/assets/6b1b3d9c-4997-4d3c-bbff-407ca1ba4c66" />

The **tuned Gradient Boosting model with a 0.30 threshold** was selected
as the final model. It achieved the highest ROC-AUC and F1-score while
maintaining substantially higher recall than Random Forest and Logistic
Regression. This provided the strongest overall balance for the
project's ranking and prioritization objective.

## Key Findings

* Historical CMS Open Payments activity contains meaningful predictive
information about future high-value status.
* Consulting activity, payment-type diversity, payment frequency, and
other recurring engagement measures were associated with future
high-value status.
* The final model achieved a **ROC-AUC of 0.8933** and identified
**69.82% of actual high-value recipients** in the independent test
set.
* The final tuned model correctly identified **118 of 169** actual
high-value recipients.
* Gradient Boosting captured nonlinear relationships and interactions
that were not fully reflected by simple linear correlations.
* Model-generated probabilities can be used to rank recipients for
further review when resources are limited.
* Results represent predictive associations and should not be
interpreted as causal relationships.

<img width="904" height="701" alt="image" src="https://github.com/user-attachments/assets/8850f7e6-401c-4f74-9b4e-60eb077d10f1" />

## Recommendations and Next Steps

The final model should be used as a ranking and prioritization tool
rather than as a standalone decision rule. Predicted probabilities can
be considered alongside professional judgment, clinical expertise, CRM
information, and other relevant organizational data.

## Future work could

* Validate the model across additional prediction years and medical
specialties
* Incorporate additional CMS Open Payments categories, including
Research Payments and Ownership Interests
* Compare model rankings with internal CRM and engagement data
* Monitor performance and retrain the model as new CMS Open Payments
data become available
* Evaluate model stability and threshold selection across future
populations

## Project Structure

The Jupyter Notebook is organized into the following sections:

1. Introduction
2. Data Engineering
3. Exploratory Data Analysis (EDA)
4. Data Preparation
5. Model Development
6. Model Evaluation
7. Prediction Validation
8. Analysis and Business Interpretation
9. Results and Discussion
10. Conclusion
11. Recommendations and Next Steps

## Project Files

* **Jupyter Notebook:**
`Predicting\_Future\_High\_Value\_Physician\_Industry\_Relationships.ipynb`
* **README:** `README.md`

## [Open in Colab](https://colab.research.google.com/drive/17YQQAHK_5ldO8yWI9ks_gVeDdzAMx3Ro#scrollTo=Yo01Ruf306ZZ)





## Author

**Colleen Yap**  
University of California, Berkeley Extension  
Professional Program in Machine Learning and Artificial Intelligence

