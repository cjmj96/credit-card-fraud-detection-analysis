# Analysis for credit card fraud detection

## Background and overview

SecureSwipe Solutions is a rapidly growing FinTech company providing
 payment processing services to online merchants and brick-and-mortar
 stores across Europe. Founded in 2020, the company has grown 
exponentially, processing hundreds of thousands of monthly 
transactions. However, with this growth, SecureSwipe has identified
 an alarming rise in fraudulent transactions, causing financial losses
 and damaging the company’s reputation among its merchant customers.


The current fraud detection system at SecureSwipe relies on static rules and is 
proving inadequate for identifying sophisticated fraud patterns. The company
 has observed that fraudsters are adapting their techniques faster than
 manual rule updates can keep up. This has resulted in false 
positives (legitimate transactions flagged as fraudulent) and 
false negatives (fraudulent transactions going undetected).

To address these challenges, SecureSwipe’s leadership has decided
 to implement a more advanced, data-driven fraud detection system
 that uses machine learning techniques. They believe that by leveraging
 the vast amount of transaction data they have accumulated, they can
 create a more accurate and adaptable fraud detection model.

This project analyzes transaction data to train a machine learning model,
 which will predict whether a transaction is fraudulent or legitimate.

The dataset used is from real anonymized transactions made by users
 in Europe. You can find the data [here](https://www.kaggle.com/code/christianmontenegro/credit-card-fraud-detection).

## Data structures and initial exploration

SecureSwipe Solutions have 568,630 credit card transactions made by European
 cardholders in 2023. It contains 31 features, divided into four groups. The first
 one uniquely identifies a transaction and only includes the id column. All 
predictors (28 features) in the second group are anonymized as 
V1, V2, ..., V28. The third group represents the transaction amount
 in Euros (Amount). The last group is the target feature (Class) using a
 binary label indicating whether the transaction is fraudulent (1) or 
not (0). The following table illustrates this:

| Feature | Purpose                                                                                  |
|----------------|---------------------------------------------------------------------------------------------|
| id             | Unique identifier for each transaction                          |
| V1             | Anonymized features representing various transaction attributes (e.g., time, location, etc.) |
| V2             | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V3             | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V4             | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V5             | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V6             | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V7             | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V8             | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V9             | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V10            | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V11            | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V12            | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V13            | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V14            | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V15            | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V16            | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V17            | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V18            | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V19            | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V20            | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V21            | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V22            | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V23            | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V24            | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V25            | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V26            | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V27            | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| V28            | Anonymized features representing various transaction attributes (e.g., time, location, etc.)  |
| Amount         | The transaction amount                                                          |
| Class          | Binary label indicating whether the transaction is fraudulent (1) or not (0)               |

The detailed report can be found on [Kaggle](https://www.kaggle.com/code/christianmontenegro/credit-card-fraud-detection). The
 open standard process model used is [CRISP-DM](https://www.datascience-pm.com/crisp-dm-2/).

## Executive summary

### Overview of Findings

The trained model achieves generalization by obtaining excellent results on different relevant performance metrics. The model
 also can be interpretable by explaining how it makes decisions to give a prediction. The following sections will provide a
 detailed explanation of this.


### Performance

The model achieved excellent performances, using AUC-ROC, sensitivity, accuracy, and F1. The scores 
were 0.99, 1, 0.99, and 0.99, respectively. Another method to evaluate our model involved the use
 of the confusion matrix. The confusion matrix indicated 24 false positives, a relatively small number
 compared to the true positives (56,976). This implies the generalizability of the model. The following image shows the confusion matrix.

![confusion-matrix](./confusion-matrix.png)

### Interpretability

The model includes interpretability capabilities by computing SHAP values. This led to the discovery that the most
 important feature, by far, for predicting whether a transaction is fraudulent or legitimate is ‘V14’ with an overall
 average SHAP value of 0.16, which is 112.5% ​​higher than the second most important feature, ‘V4’ with 0.08. It is important
 to note that the least important feature for the model’s objective prediction is the amount of money 
transferred (‘Amount’). The following image illustrates this.

![Global-explanation-using-shap](./Global-explanation-using-shap.png)

At the individual predictive level, it allows us to understand a particular decision in more detail for customer
 trust and transparency. When a transaction is labeled as potentially fraudulent, providing a clear
 and understandable explanation can help maintain customer trust. The following waterfall chart illustrates
 how the model decides to predict correctly that a transaction is fraudulent.

![waterfall-chart](./waterfall-chart.png)

## Recommendations and future steps

Based on the knowledge gained about fraudulent and legitimate transaction patterns, by training a predictive
 model with generalization and interpretability capabilities, using gradient boosted decision trees (GBDT), 
implemented in XGBoost, some practical recommendations are offered below:

- Deploy model in production: Based on the results obtained, the model is robust enough to replace the 
current static rules system. It is recommended to proceed with the implementation of the model at 
the production level to improve fraud detection and reduce financial losses.

- Optimize the customer interface based on interpretability: Create a clear and simple interface that
 explains the model’s decisions to merchants and customers. For example, if a transaction is classified
 as suspicious, the system should be able to explain the main reasons for such a classification using
 key features (such as ‘V14’) with understandable explanations. This is essential to maintain customer
 trust when a legitimate transaction is flagged as potentially fraudulent. Real-time notifications should
 also be implemented so that customers can immediately review transactions labeled as suspicious,
 and provide an efficient system for them to quickly confirm or refute the decision.

- Provide support and feedback: Implement an active support system so that customers of payment
 processing companies can quickly report problems or concerns about the fraud detection system. This
 feedback can be valuable in improving both the model and the customer experience.

- Monitor key metrics in production: Although the model has shown a high rate of accuracy and sensitivity,
 it is essential to continuously monitor its performance in production. Fraud threats evolve rapidly, so it is
 recommended to implement a monitoring system that tracks metrics such as the false positive and 
negative rate, the rate of fraud detected, and financial losses avoided.

- Retrain the model periodically: As more transaction data accumulates, it is important to retrain the 
model regularly so that it continues to learn from new fraud patterns and does not become obsolete. A
 retraining cycle is recommended periodically, for example, every 3-6 months, or when key performance
 indicators deteriorate.

- Manually review important false negatives: Although the model shows high sensitivity, it is critical to
 have a dedicated team manually review transactions that are not flagged as suspicious by the model
 but are subsequently identified as fraudulent by clients or audit systems. These cases can provide 
valuable feedback for fine-tuning the model.

- Focus on key features: The analysis showed that feature ‘V14’ is the most relevant for fraud detection,
 with an overall average SHAP value of 0.17, markedly higher than the other features. A deeper analysis
 of what this feature represents and how its data collection or representation in the system can be
 improved is recommended. Furthermore, since the amount of money transferred (‘Amount’) was
 identified as the least important feature, the weight assigned to this variable in other decision systems could be reconsidered.

- Explore new features: As SecureSwipe grows, it is important to explore the possibility of integrating
 new features that could further improve the model’s accuracy. This could include geographic data,
 user behavior patterns, or transaction times.