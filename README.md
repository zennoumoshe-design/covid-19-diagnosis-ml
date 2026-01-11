# COVID-19 Diagnosis Prediction using Machine Learning

## Project Overview
The objective of this project is to build a data-driven machine learning model capable of predicting whether a patient is COVID-19 positive or negative based on available clinical, blood test, and viral test data.

Beyond model performance, this project places strong emphasis on **data understanding, analytical reasoning, and decision-making**, following an end-to-end data science workflow: from exploratory data analysis to model optimization and final business-oriented decisions.

This approach ensures that the project remains relevant for both **Data Analyst** and **Data Scientist** roles.

---

## Business Objective & Evaluation Metrics
**Objective:**  
Predict whether a patient is infected with COVID-19 based on clinical and biological features.

**Key challenge:**  
The dataset is highly imbalanced (~10% positive cases) and contains a large proportion of missing values, making prediction non-trivial.

**Evaluation metrics:**  
- **F1-score** (target ≥ 50%) to balance precision and recall  
- **Recall** (target ≥ 70%) to minimize false negatives, which is critical in a medical screening context

---

## Dataset Description & Challenges
- Source: Kaggle – COVID-19 clinical diagnosis dataset  
- Observations: 5,644 patients  
- Features: 111 variables (blood tests, viral tests, age, hospitalization data)

**Main challenges identified:**
- Over 50% of the variables contain more than 90% missing values  
- Strong class imbalance (≈ 90% negative, 10% positive)  
- Limited signal in several clinical variables

These constraints strongly influenced the analytical and modeling strategies adopted in this project.

---

## Exploratory Data Analysis (EDA)
The EDA phase aimed to understand the structure, limitations, and potential predictive power of the data.

Key steps included:
- Target distribution analysis and imbalance assessment  
- Missing value analysis by feature groups (blood tests, viral tests)  
- Distribution analysis of continuous variables  
- Feature–target relationship exploration  
- Correlation analysis between variables  
- Statistical hypothesis testing (t-tests) on selected blood markers  

**Key analytical insights:**
- Platelets, Leukocytes, and Monocytes show statistically significant differences between COVID-positive and negative patients  
- Age has limited correlation with blood markers  
- Viral co-infections are rare and not strongly predictive of COVID status  
- The dataset contains limited but non-random signal, justifying further modeling efforts

---

## Data Preprocessing
To prepare the dataset for machine learning, several preprocessing steps were applied:

- Removal of features with more than 90% missing values  
- Encoding of categorical variables into numeric format  
- Handling of missing values using controlled strategies  
- Train/Test split (80% / 20%) with preserved class distribution  
- Feature engineering (e.g., creation of aggregated health indicators)  
- Feature selection using statistical tests (ANOVA – SelectKBest)

All preprocessing steps were designed to ensure **consistency between training and testing data** and prevent data leakage.

---

## Modeling Strategy
The modeling phase followed an iterative and diagnostic-driven approach:

1. **Baseline model:** Decision Tree (fast diagnostic model)
2. **Model diagnosis:** Learning curves revealed strong overfitting
3. **Iterative improvements:**
   - Feature engineering
   - Feature selection
   - Dimensionality reduction
4. **Model comparison:**
   - Random Forest
   - AdaBoost
   - Support Vector Machine (SVM)
   - K-Nearest Neighbors (KNN)

Each model was evaluated using consistent metrics and learning curve analysis.

---

## Model Optimization
The **Support Vector Machine (SVM)** emerged as the most promising model.

Optimization techniques included:
- Feature selection tuning (`k` parameter)
- Polynomial feature expansion
- Hyperparameter optimization using:
  - GridSearchCV
  - RandomizedSearchCV (for computational efficiency)

**Optimized configuration:**
- Kernel: Polynomial  
- Gamma: 0.001  
- C: 1000  
- Selected features: 51  
- Polynomial degree: 3  

---

## Threshold Optimization & Business Decision
Instead of relying solely on the default classification threshold, a **Precision–Recall curve analysis** was performed.

Key insight:
- A very low threshold yields perfect recall but unacceptable precision  
- The optimal trade-off depends on the business objective  

Given the medical screening context, recall was prioritized over precision.

**Final decision threshold:** `-0.7`

---

## Final Results
With the optimized SVM model and adjusted threshold:

- **F1-score:** 64.9% (objective achieved)  
- **Recall:** 75% (objective achieved)  

These results demonstrate that, despite data limitations, a carefully designed analytical and modeling strategy can extract meaningful predictive signal.

---

## Key Takeaways
- Strong EDA is critical when working with noisy and incomplete medical data  
- Model performance alone is insufficient without diagnostic analysis  
- Feature selection and threshold tuning had greater impact than model complexity  
- Business objectives should directly guide evaluation metrics and decision thresholds  

---

## Repository Structure

```
├── notebooks/
│   └── DiagnosisOfCOVID19_EN.ipynb
├── data/
│   └── DatasetCovid19.xlsx
├── reports/
│   └── project_summary.md
├── README.md
└── requirements.txt
```

