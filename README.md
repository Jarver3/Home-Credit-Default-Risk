# Home-Credit-Default-Risk
## Project Description
This repository is a simplified version of my solution to Kaggle competition ["Home credit default risk"](https://www.kaggle.com/competitions/home-credit-default-risk/overview). The competitors are asked to predict the Home Credit's clients repayment abilities, given customer's current application, as well as previous loan records, credit accounts information at other institutions and monthly payment data in the past. The predictions are evaluated on area under the ROC curve between the predicted probability and the observed target.
#### Dataset
* **application_{train|test}.csv**
Contains the main application data with client-level information for training and testing, including demographic, financial, and loan-related details.
* **bureau.csv**
Records clients' previous credit information from other financial institutions, including loan status and credit history.
* **bureau_balance.csv**
Monthly updates of the status of loans recorded in the *bureau.csv*.
* **POS_CASH_balance.csv**
Contains monthly records of point-of-sale (POS) or cash loan repayments made by the clients.
* **credit_card_balance.csv**
Monthly credit card balance details, including payment amounts, limits, and overdue status.
* **previous_application.csv**
Data on previous loan applications made by clients, including application outcomes and associated financial information.
* **installments_payments.csv**
Detailed records of loan installment payments, showing whether payments were made on time.
![image](https://github.com/user-attachments/assets/8dcd9c50-f20c-4d2d-adb1-18f8216e1ca8)
#### Final score for the full solution:
Private LB: 0.78651 Public  LB: 0.79008

## Project Design and Solution
1. <u>**Data Preparation**</u> - Before modeling, it is essential to import all necessary datasets and libraries, then inspect the feature types and the number of rows and columns in each dataset.

2. <u>**Exploratory Data Analysis**</u> - Perform EDA to understand the data structure and quality. Evaluate the number of features, their types, missing values, and class imbalances. Analyze relationships between predictors and the target variable to identify potential patterns.

3. <u>**Feature Engineering**</u> - Based on the EDA results, feature engineering can be performed by handling outliers, imputing missing values, and processing categorical variables using methods like Label Encoding or One-Hot Encoding. Additionally, statistical methods (e.g., min, max, mean, sum, variance) can be applied to combine information from multiple tables. Domain knowledge in finance can also be used to create new features. Finally, features with high correlations (corr > 0.8) should be removed to solve co-linear problem.

4. <u>**Classifier Models**: Due to the class imbalance (0: non-default >> 1: default), it is essential to address this issue during model training. After splitting the data into training and test sets, various classification models (e.g., Logistic Regression, XGBoost, LightGBM, Deep Learning) can be trained and evaluated using the ROC AUC metric. K-fold cross-validation ensures robust parameter selection for better generalization. Features with zero importance, identified through feature importance and SHAP analysis, can be removed. Additionally, blending or stacking multiple models can be applied to enhance prediction accuracy.

5. <u>**Hyperparameter Tuning**</u> - First, use Random Search and manual tuning to select initial hyperparameters. Then, apply Bayesian Optimization to explore the defined parameter space for the optimal combination. By monitoring the changes in ROC AUC scores across iterations, the most effective set of hyperparameters can be identified.


