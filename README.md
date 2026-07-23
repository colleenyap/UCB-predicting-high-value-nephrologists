# UCB-predicting-high-value-nephrologists
Predicting Future High-Value Physician–Industry Relationships Among Nephrologists Using CMS Open Payments Data

Author
Colleen Yap

Executive Summary

The goal of this project is to determine whether historical physician–industry payment patterns can be used to predict which nephrologists will become high-value industry partners in the following year. Using publicly available CMS Open Payments General Payments data, I developed a complete machine learning workflow that included SQL-based data engineering, feature engineering, exploratory data analysis (EDA), predictive modeling, and model evaluation. Historical payment data from 2020–2023 were used to create physician-level features, while 2024 payment data served as the prediction target. Among the models evaluated, Gradient Boosting delivered the strongest performance with a ROC-AUC of 0.9068, demonstrating that historical physician–industry engagement is a strong predictor of future high-value industry relationships.

Rationale

The CMS Open Payments program provides transparency into financial relationships between physicians and life sciences companies, but it is primarily used to report historical transactions. This project explores whether those historical records can also be used to predict future physician–industry engagement.
For biotechnology and pharmaceutical companies developing kidney disease therapies, identifying physicians who are likely to become highly engaged with industry can support more informed commercial and medical affairs planning. Rather than relying solely on past payment reports, predictive analytics can help identify physicians who may become future collaborators, speakers, educators, or research partners.

Research Question

Can historical physician–industry payment patterns from 2020–2023 be used to predict which nephrologists will receive high-value industry payments in 2024?
Data Sources
The project uses publicly available CMS Open Payments General Payments datasets obtained from the Centers for Medicare & Medicaid Services (CMS).

Source:

https://openpaymentsdata.cms.gov/

Data included:

•	CMS Open Payments General Payments (2020–2024)
•	Physician specialty: Nephrology
Historical payment data from 2020–2023 were used to engineer physician-level predictor variables, while the 2024 General Payments dataset was used to construct the target variable and evaluate model performance.
Methodology
The project followed a complete end-to-end machine learning workflow.
Data Engineering
A seven-step SQL data pipeline was developed to:
•	Combine annual CMS Open Payments datasets from 2020 to 2024
•	Filter records to nephrology physicians
•	Aggregate physician payment history
•	Engineer historical physician features
•	Create the 2024 prediction target
•	Build the final machine learning dataset

Exploratory Data Analysis

EDA included:
•	Dataset overview
•	Missing value analysis
•	Duplicate record validation
•	Summary statistics
•	Payment distributions
•	Target class distribution
•	Correlation analysis
•	Geographic analysis
•	Historical payment behavior

Machine Learning

The following classification models were developed and compared:
•	Logistic Regression
•	Decision Tree
•	Random Forest
•	Gradient Boosting

Model performance was evaluated using:
•	Accuracy
•	Precision
•	Recall
•	F1-score
•	ROC-AUC
•	Confusion Matrix
•	ROC Curve
•	Feature Importance

Results

The final modeling dataset contained 11,044 physicians, with historical features derived from 2020–2023 and a binary target representing high-value physicians in 2024.
A physician was classified as high value if total 2024 General Payments were at or above the 90th percentile ($2,057.67).
Among the four machine learning models evaluated, Gradient Boosting achieved the strongest overall performance:
•	ROC-AUC: 0.9068
•	Recall: 0.7824
•	F1-score: 0.5648

The results show that historical physician–industry engagement, including payment history, consulting activity, and the breadth of industry relationships - provides meaningful predictive information for identifying physicians who are likely to become high-value industry partners.

Next Steps
Future work may include:
•	Expanding the analysis to additional physician specialties.
•	Validating the model using future CMS Open Payments releases.
•	Comparing model predictions with internal CRM data to evaluate physician engagement strategies.

Outline of Project
•	Introduction
•	Data Engineering
•	Exploratory Data Analysis (EDA)
•	Machine Learning Model Development
•	Model Evaluation
•	Results
•	Discussion
•	Conclusion

Project Files
•	Jupyter Notebook: Predicting_Future_High_Value_Physician–Industry_Relationships_Among_Nephrologists_Using_CMS_Open_Payments_Data.ipynb

Contact and Further Information

Author: Colleen Yap
Program: University of California, Berkeley Extension
Course: Professional Program in Machine Learning and Artificial Intelligence
