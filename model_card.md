# Customer Churn Prediction Model Card

## Model Overview

This model predicts whether a customer will churn within the next 60 days. The model is intended to help retention, marketing, and CRM teams prioritize intervention efforts.

## Intended Use

The model should be used to:

* Identify customers at elevated churn risk
* Prioritize retention campaigns
* Support CRM decision making
* Allocate retention budgets efficiently

The model should not be used as the sole basis for customer treatment decisions.

## Data Used

Dataset: rfm_modeling_snapshot.csv

Target Variable:

* churn_next_60d

Features Used:

* Customer profile attributes
* RFM metrics
* Support ticket behavior
* Product engagement metrics
* Marketing engagement metrics
* Loyalty information

## Leakage Prevention

Only information available on or before the customer snapshot date was used.

The following fields were excluded from modeling:

* customer_id
* snapshot_date
* split
* target label

No post-snapshot behavior was used as input.

## Models Evaluated

1. Logistic Regression
2. Random Forest

## Final Model Selected

Logistic Regression

Reason:

Although both models performed well, Logistic Regression achieved the highest ROC-AUC score while providing superior interpretability and easier deployment.

## Performance

 Metric    | Value  |

 Accuracy   0.8155 
 Precision  0.7819 
 Recall     0.8750 
 F1 Score   0.8258 
 ROC-AUC    0.8870 

## Threshold Selection

Threshold = 0.40

The threshold was selected to prioritize recall because missing a likely churner creates greater business cost than contacting an additional customer.

## Key Drivers

Top churn indicators:

* return_rate_180d
* avg_discount_pct_180d
* negative_ticket_rate_90d
* ticket_count_90d
* category_diversity_180d

Top retention indicators:

* loyalty_tier_Platinum
* acquisition_channel_Organic
* marketing_consent_Yes
* campaign_clicks_30d
* frequency_180d

## Limitations

* Customer behavior may change over time.
* Performance may degrade if customer acquisition channels change.
* New customers with limited history may be difficult to classify.
* Predictions should be periodically recalibrated.

## Ethical Considerations

* Predictions should not be used to deny service.
* Predictions should not be used to penalize customers.
* Human review should remain part of retention decision making.
* Customers should not receive materially different treatment solely due to model output.

## Monitoring Recommendations

Monitor:

* Prediction distribution
* Churn rate
* Recall and precision
* Feature drift
* Customer response to retention campaigns

Model retraining should be considered when significant performance degradation or feature drift is observed.
