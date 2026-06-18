# Error Analysis

## Overview

The final Logistic Regression model achieved:

* Accuracy: 81.55%
* Precision: 78.19%
* Recall: 87.50%
* F1 Score: 82.58%
* ROC-AUC: 88.70%

A threshold of 0.40 was selected to prioritize recall and identify as many potential churners as possible.


# False Positive Analysis

False positives are customers predicted to churn who ultimately did not churn.

Business Impact:

* Unnecessary retention incentives
* Additional marketing costs
* Reduced campaign efficiency

However, false positives are generally less costly than false negatives because the customer remains active.

 Customer ID  Churn Probability  Interpretation                                                                                                    

 CUST00044    0.4065             Borderline churn signal likely triggered by temporary inactivity.                                                 
 CUST00109    0.5042             Moderate churn risk indicators present, but customer remained engaged.                                            
 CUST00248    0.5095             Model detected behavior similar to historical churners.                                                           
 CUST00335    0.7585             Strong churn signals observed, but customer was retained.                                                         
 CUST00437    0.9274             Very high predicted risk despite eventual retention, suggesting successful customer recovery or unusual behavior. 

Observation:

Several false positives exhibited meaningful churn-like behavior. These customers may still represent a useful retention audience because they share characteristics with actual churners.



# False Negative Analysis

False negatives are customers predicted to stay who ultimately churned.

Business Impact:

* Lost revenue
* Lost customer lifetime value
* Missed retention opportunities

False negatives are generally the more expensive error type.

 Customer ID  Churn Probability  Interpretation                                                         

 CUST00088    0.3669             Churn occurred despite moderate retention indicators.                  
 CUST00184    0.0622             Customer exhibited very few warning signs before churning.             
 CUST00247    0.2808             Hidden churn drivers may not be captured by available features.        
 CUST00568    0.3890             Customer fell just below the selected decision threshold.              
 CUST00592    0.2322             Unexpected churn behavior not reflected in historical engagement data. 

Observation:

False negatives suggest that some churn events are driven by factors not present in the dataset, such as competitor offers, personal preferences, or external circumstances.



# Key Learnings

1. Customer dissatisfaction signals such as returns and support interactions are highly predictive.
2. Engagement metrics substantially improve churn detection.
3. Some churn events remain difficult to predict due to unobserved factors.
4. The chosen threshold favors recall and reduces the number of missed churners.
5. Future improvements could include additional behavioral, transactional, or survey-based features.
