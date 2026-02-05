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
1. Cholesterol (chol)
- Important clinical indicator for heart disease.
- Showed some signal in EDA but worked better when combined with other factors.
1. Blood Pressure (trestbps)
- Showed clearer separation between risk groups compared to many other features.
- Clinically relevant and commonly used in risk assessment.
1. Diabetes (diabetes)
- Long-term health condition linked to heart disease.
- Increased risk when present, especially with other factors.
1. Smoking (smoking)
- Known lifestyle risk factor.
- Included to capture cumulative lifestyle effects, even though its individual impact was weaker in this dataset.
1. Obesity (obesity)
- Associated with higher cardiovascular risk.
- Interacts with diabetes and cholesterol.

These variables represent a mix of clinical measurements and lifestyle conditions, which aligns with real-world heart-risk assessment.

#### How the combinations were created #### 
1. Cholesterol and blood pressure were grouped into medically meaningful categories:
- Normal
- Borderline / Elevated
- High
1. Lifestyle risk was summarized using a combined score based on:
- Diabetes
- Smoking
- Obesity
1. Lifestyle groups were defined as:
- No Lifestyle Risk Factors
- One Lifestyle Risk Factor
- Multiple Lifestyle Risk Factors
  
Above approach resulted easier risk calculation and clear data rather than analyzing too many individual variables.



