# Project Summary – COVID-19 Diagnosis Prediction

## 1. Problem Definition & Objectives
The objective of this project is to predict whether a patient is COVID-19 positive or negative using available clinical, blood test, and viral test data.

From a business and medical perspective, the main challenge is to **minimize false negatives**, as failing to detect a positive patient can have serious public health consequences. Therefore, the project explicitly prioritizes recall while maintaining an acceptable balance with precision.

Target performance objectives:
- **F1-score ≥ 50%**
- **Recall ≥ 70%**

---

## 2. Dataset Overview & Limitations
The dataset contains **5,644 patients and 111 variables**, including blood test results, viral test indicators, age information, and hospitalization data.

Key limitations identified early in the analysis:
- Strong class imbalance (~90% negative, ~10% positive)
- Extremely high proportion of missing values (over 50% of features have more than 90% missing data)
- Limited domain context for certain variables (e.g. age quantile encoding)

These constraints required a cautious and well-justified analytical and modeling strategy.

---

## 3. Exploratory Data Analysis (EDA) – Key Findings
The EDA phase focused on understanding the structure, quality, and predictive potential of the data.

Main insights:
- Several blood markers (Platelets, Leukocytes, Monocytes) show statistically significant differences between COVID-positive and negative patients
- Age has limited correlation with blood test values
- Viral co-infections are rare and do not provide strong predictive signal for COVID-19
- Many variables contain noise or insufficient signal, reinforcing the need for feature selection

Despite these limitations, the data contains **non-random patterns** that justify further modeling efforts.

---

## 4. Hypotheses & Statistical Testing
Based on the EDA, multiple hypotheses were formulated and tested.

Example hypothesis:
- *Blood marker levels (Platelets, Leukocytes, Monocytes) differ significantly between COVID-positive and negative patients.*

Using t-tests:
- The null hypothesis of equal means was rejected, confirming statistically significant differences.

This step helped validate that observed patterns were not due to random variation.

---

## 5. Data Preprocessing & Feature Engineering
To prepare the data for machine learning:
- Features with more than 90% missing values were removed
- Categorical variables were encoded into numeric format
- Missing values were handled using controlled strategies
- An 80/20 train-test split was applied while preserving class distribution

Additional steps included:
- Creation of aggregated health indicators (e.g. “is sick” variable)
- Feature selection using ANOVA-based SelectKBest
- Polynomial feature expansion to capture non-linear relationships

All preprocessing steps were applied consistently to avoid data leakage.

---

## 6. Modeling Strategy & Iterations
The modeling process followed an iterative and diagnostic-driven approach.

Steps:
1. Baseline model using a Decision Tree to quickly diagnose model behavior
2. Learning curve analysis revealing strong overfitting
3. Progressive improvements through feature engineering and feature selection
4. Comparison of multiple models:
   - Random Forest
   - AdaBoost
   - Support Vector Machine (SVM)
   - K-Nearest Neighbors (KNN)

Model evaluation relied on F1-score, recall, and learning curves rather than accuracy alone.

---

## 7. Model Optimization & Threshold Selection
The Support Vector Machine (SVM) emerged as the most robust model.

Optimization included:
- Hyperparameter tuning using GridSearchCV and RandomizedSearchCV
- Reduction of feature space to the most informative variables
- Polynomial kernel configuration

Rather than relying on the default classification threshold, a **Precision–Recall curve analysis** was performed.

Given the project objective, recall was prioritized over precision. A custom decision threshold was selected to reflect this trade-off.

---

## 8. Final Results & Interpretation
With the optimized SVM model and adjusted decision threshold:

- **F1-score:** 64.9%
- **Recall:** 75%

Both predefined objectives were achieved.

These results demonstrate that, despite significant data limitations, a structured analytical approach combined with careful model diagnostics and threshold tuning can produce meaningful and actionable predictions.

---

## 9. Project Limitations & Next Steps
Key limitations:
- High level of missing data
- Limited clinical context for certain variables
- Dataset not representative of a real-world screening population

Potential next steps:
- Collection of more complete and clinically rich data
- Exploration of advanced imputation techniques
- External validation on independent datasets
- Deployment-oriented evaluation (cost-sensitive learning)

---

## Conclusion
This project highlights the importance of combining **strong exploratory data analysis**, **statistical reasoning**, and **iterative machine learning optimization**.

Rather than focusing solely on model complexity, the project emphasizes **data understanding, diagnostic analysis, and business-driven decision-making**, making it relevant for both Data Analyst and Data Scientist roles.
