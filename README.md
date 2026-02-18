# Capstone Project : Heart Attack Risk Prediction #

## Problem Context ##

India is dealing with a big rise in two major health issues: Type 2 Diabetes and heart disease.

These two problems are very connected. If you can't control your blood sugar, you're much more likely to have a heart attack. So, to deal with one, you have to understand the other.

The goal is to move from just reacting to emergencies (like a heart attack) to a more proactive approach. This means identifying people who are at high risk early on and helping them with preventative care to stop these problems before they start.

#### Problem statement ####

"How accurately can we use AI to predict heart attack risk for people in India? And when we look at all the health factors, just how much bigger of a red flag is diabetes compared to everything else?"

#### Data Source ####

Dataset: https://www.kaggle.com/datasets/khushikyad001/heart-attack-risk-prediction-dataset-india

## Exploratory Data analysis ##

#### Step 1 : Prepare the data ####
     1. Load the heart-attack dataset and checked its shape (rows and columns).
     2. Review the target column to see how many low-risk and high-risk patients exist
     3. Checked for missing values and duplicate rows.
     4. This step helps make sure the data is clean enough to continue with analysis

#### Step 2 : Exploratory Data Analysis: Key Combinations (Cholesterol, Blood Pressure, Lifestyle) ####
- Initial Analysis showed that many individual features did not clearly separate low-risk and high-risk patients.
- Risk patterns became clearer when multiple factors were analyzed together.
- Based on this,  understanding how clinical factors and lifestyle factors interact becomes important in considering the risk factors

#### What and why - specific columns were selected ####
The following columns were used for combination analysis:
- Cholesterol (chol)
    - Important clinical indicator for heart disease.
    - Showed some signal in EDA but worked better when combined with other factors.
- Blood Pressure (trestbps)
    - Showed clearer separation between risk groups compared to many other features.
    - Clinically relevant and commonly used in risk assessment.
- Diabetes (diabetes)
    - Long-term health condition linked to heart disease.
    - Increased risk when present, especially with other factors.
- Smoking (smoking)
    - Known lifestyle risk factor.
    - Included to capture cumulative lifestyle effects, even though its individual impact was weaker in this dataset.
- Obesity (obesity)
    - Associated with higher cardiovascular risk.
    - Interacts with diabetes and cholesterol.

These variables represent a mix of clinical measurements and lifestyle conditions, which aligns with real-world heart-risk assessment.

#### How the combinations were created #### 
- Cholesterol and blood pressure were grouped into medically meaningful categories:
    - Normal
    - Borderline / Elevated
    - High
- Lifestyle risk was summarized using a combined score based on:
    - Diabetes
    - Smoking
    - Obesity
- Lifestyle groups were defined as:
    - No Lifestyle Risk Factors
    - One Lifestyle Risk Factor
    - Multiple Lifestyle Risk Factors
  
Above approach resulted easier risk calculation and clear data rather than analyzing too many individual variables.


## Models - Performance interpretation  ##

To evaluate the performance and identify suitable model, following five metrics are used -
- Accuracy
- Precision
- Recall
- F1-Score
- AUC

####  Accuracy - Indicates overall correctness ####
Accuracy measures the percentage of total predictions that were correct.
- Higher accuracy means the model correctly predicts more cases overall.
- However, accuracy alone can be misleading if the dataset has overlapping patterns or class imbalance.
- In healthcare prediction tasks, accuracy should be interpreted together with Recall and AUC.


####  Precision - Shows prediction reliability ####
Precision measures how many of the predicted high-risk patients were actually high risk.

$$Precision = True Postive / Predicted Postive$$

- Higher the precision means, fewer false alarams
- Useful when false positives are costly
- Precision alone does not denote whether the model is missing high risk patients


####  Recall - Measures risk detection ability ####
Recall measures how many of the actual high-risk patients were successfully detected by the model.

$$Recall = True Postive / Actual Postive$$

- Higher recall means the model detects more high-risk individuals.
- In healthcare, recall is often more important than accuracy because missing a high-risk patient can be serious.

####  F1-Score - Balances precision and recall ####
F1-score is the harmonic mean of Precision and Recall.

$$F1-Score = 2 * ((Precision * Recall)/(Precision + Recall))$$

- Provides a balanced measure when both false positives and false negatives matter.
- Useful for comparing models when there is no single dominant metric.
- F1-scores were used to compare overall classification balance across models.


####  AUC - Evaluates overall ranking performance ####
AUC measures how well the model separates high-risk and low-risk patients across all classification thresholds.

- Higher AUC indicates better ranking ability.
- AUC is especially useful when the goal is to prioritize high-risk patients rather than make a single yes/no decision.


## Models  ##
Used a 60% train, 25% validation, and 15% test split.

#### Baseline : Decision Tree ####
- Trained a simple Decision Tree model as a baseline.
- Evaluated the model using accuracy, precision, recall, and F1-score.
- The model achieved limited accuracy, which suggests underfitting.


####  Logistic Regression ####
- This model predicts heart-attack risk using a linear combination of features.
- It is easy to understand and interpret.
- However, it assumes mostly linear relationships between features and the target.
- Because healthcare data often contains complex interactions, the model showed moderate performance.


####  Polynomial Logistic Regression: ####
- Added Polynomial Features (degree = 2) before Logistic Regression.
- This allows the model to capture interaction effects between features.
- Compared to the basic Logistic Regression, this model improved recall, meaning it identified more high-risk patients.
- This shows that feature interactions are important for predicting heart-attack risk.

####  Random Forest ####
- Random Forest is an ensemble method that builds many decision trees and combines their predictions.
- It automatically captures non-linear relationships and feature interactions.
- Compared to a single Decision Tree, Random Forest produced more stable and better overall performance.

####  Gradient Boosting ####
- Gradient Boosting builds decision trees sequentially, where each new tree learns from the errors of the previous trees.
- It performs well for structured healthcare datasets because it can capture non-linear relationships and interactions between multiple risk factors.
- In this project, Gradient Boosting achieved strong overall ranking performance (high AUC) and maintained balanced Accuracy, Precision, and Recall.
- It serves as a reliable ensemble benchmark model for comparison.

####  XGBoost ####
- XGBoost (Extreme Gradient Boosting) is an optimized implementation of the Gradient Boosting algorithm that improves training efficiency and predictive performance.
- In this project, XGBoost achieved the highest Recall, meaning it detected more patients who are at high risk of heart attack.
- It also maintained competitive AUC and Accuracy, indicating strong overall predictive capability.

**Because detecting high-risk patients is the primary objective, XGBoost is selected as the recommended final model, while Gradient Boosting remains a strong alternative model.**




