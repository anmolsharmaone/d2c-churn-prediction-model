# d2c-churn-prediction-model
# D2C Customer Churn Prediction Model

This repository contains my submission for Part 3 of the D2C Customer Churn Intelligence & Retention Capstone Project.

The objective was to build a machine learning model capable of identifying customers who are likely to churn in the next 60 days so that the business can take proactive retention actions instead of applying discounts to every customer.

## Problem Statement

The D2C brand wants to reduce customer churn by identifying customers at risk before they leave. The prediction system should help marketing, CRM, and retention teams focus their efforts on customers who need intervention.

The target variable for this project is:

`churn_next_60d`

A value of 1 indicates that the customer churned within the following 60 days, while 0 indicates that the customer remained active.

## Dataset Used

The provided `rfm_modeling_snapshot.csv` dataset contains customer-level features generated before the prediction window.

The dataset includes:

* Customer profile attributes
* Acquisition channel information
* Loyalty membership details
* RFM metrics
* Product category preferences
* Support ticket activity
* Return and refund behavior
* Website and app engagement metrics
* Campaign interaction metrics

The dataset contains 2400 customer records.

## Leakage Prevention

One of the most important requirements of this capstone was avoiding data leakage.

Only information available on or before the snapshot date was used for prediction.

The following fields were excluded from training:

* customer_id
* snapshot_date
* split
* churn_next_60d

No future customer activity was used as an input feature.

## Modeling Approach

The dataset already included predefined train, validation, and test splits.

Training records: 1728

Validation records: 336

Test records: 336

Two models were developed and evaluated:

1. Logistic Regression
2. Random Forest

Categorical variables such as city tier, acquisition channel, loyalty tier, preferred category, and marketing consent were encoded using One-Hot Encoding before training.

## Model Comparison

Both models produced strong results.

Logistic Regression achieved a ROC-AUC score of 0.8870.

Random Forest achieved a ROC-AUC score of 0.8848.

Although the difference was small, Logistic Regression performed slightly better and was selected as the final model because it also provides easier business interpretation.

## Final Model Performance

The final Logistic Regression model achieved:

Accuracy: 81.55%

Precision: 78.19%

Recall: 87.50%

F1 Score: 82.58%

ROC-AUC: 88.70%

A decision threshold of 0.40 was selected because the business objective is customer retention. Missing a customer who is about to churn is generally more expensive than contacting an additional customer who may not actually churn.

## Key Findings

Several behavioral patterns showed a strong relationship with churn risk.

Customers with higher return rates were significantly more likely to churn.

Customers receiving large discounts over long periods also showed elevated churn risk, suggesting dependence on promotional offers.

Negative support experiences were another major churn signal. The negative ticket rate and support-related features consistently appeared among the strongest predictors.

On the other hand, customers who actively engaged with campaigns, belonged to higher loyalty tiers, and purchased more frequently were generally less likely to churn.

Some of the most influential features identified by the model were:

* return_rate_180d
* avg_discount_pct_180d
* negative_ticket_rate_90d
* ticket_count_90d
* category_diversity_180d
* campaign_clicks_30d
* frequency_180d

These findings align closely with the business hypotheses developed during the earlier stages of the capstone.

## Repository Contents

`churn_model.ipynb`

Contains the complete modeling workflow including preprocessing, model training, evaluation, threshold analysis, feature interpretation, and model export.

`model.pkl`

Serialized final Logistic Regression model.

`metrics.json`

Performance metrics generated from the test dataset.

`error_analysis.md`

Analysis of false positives and false negatives along with customer-level examples.

`model_card.md`

Documentation describing intended use, limitations, ethical considerations, and monitoring recommendations.

`requirements.txt`

Project dependencies.

## How to Run

Install the required packages:

```bash
pip install -r requirements.txt
```

Open and execute:

```bash
jupyter notebook churn_model.ipynb
```

Running the notebook will reproduce the training process and generate the model artifacts.

## Conclusion

The final model demonstrates strong performance for churn prediction and can be used to support targeted retention campaigns. The results suggest that customer dissatisfaction, return behavior, discount dependence, and declining engagement are among the strongest indicators of future churn. These insights can help the business focus retention efforts on customers most likely to leave while avoiding unnecessary interventions for low-risk customers.
