<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/74038190/212284113-b336b21d-7334-451e-9188-59298a1f2905.gif" alt="logo" width="600" height="300">
</p>
<h1 align="center">Heart Failure Prediction</h1>
<p align="center">
  A machine learning project to predict mortality by heart failure using clinical records.
</p>

<p align="center">
    <img src="https://www.r-project.org/logo/Rlogo.png" alt="R" height="28">
    <img src="https://img.shields.io/badge/Model-Random_Forest-2ea44f?style=for-the-badge" alt="Model">
    <img src="https://img.shields.io/badge/Accuracy-81.33%25-blue?style=for-the-badge" alt="Accuracy">
</p>

## 📖 Table of Contents
*   [Abstract](#-abstract)
*   [Background](#-background)
*   [Dataset](#-dataset)
*   [Exploratory Data Analysis (EDA)](#-exploratory-data-analysis-eda)
*   [Methodology](#-methodology)
    *   [Data Pre-processing](#data-pre-processing)
    *   [Feature Selection](#feature-selection)
    *   [Model Selection](#model-selection)
*   [Final Model & Results](#-final-model--results)
*   [Conclusion](#-conclusion)
*   [Future Scope](#-future-scope)
*   [Download Full Report (PDF)](#-Download-Full-Report)
*   [Author](#-author)


## 📜 Abstract

Heart failure is a life-threatening cardiovascular ailment with a major effect on global public health. This project investigates the predictive value of key clinical markers like **serum creatinine**, **ejection fraction**, and **follow-up time** to determine the likelihood of mortality due to heart failure. By leveraging machine learning models, we aim to predict whether a patient is at high risk, enabling timely preventative approaches and therapies.

## 🔬 Background

Cardiovascular diseases, leading to myocardial infarctions and heart failure, account for over 17 million deaths annually worldwide. Heart failure is a clinical illness where the heart cannot pump enough blood to meet the body's metabolic needs. Despite advancements in understanding its mechanisms and treatments, heart failure carries a 50% mortality rate within a five-year span.

This project builds upon existing research which identifies a broad set of predictors but lacks consensus on their relative impact. By focusing on a reproducible methodology, we aim to build a robust model using the most significant clinical features.

## 📊 Dataset

The dataset was sourced from the Government College University, Faisalabad-Pakistan, and contains records of 299 heart patients. The study was approved by an Institutional Review Board, adhering to the Helsinki Declaration.

**Dataset Characteristics:**
*   **Instances:** 299
*   **Subjects:** 194 men, 105 women
*   **Age Range:** 40-95 years
*   **Follow-up Period:** 4 to 285 days
*   **Target Variable:** `DEATH_EVENT` (if the patient died during the follow-up)

### Feature Descriptions

| Feature | Explanation | Measurement | Type |
| :--- | :--- | :--- | :--- |
| **Age** | Age of the patient | Years | Continuous |
| **Anaemia** | Decrease of red blood cells or haemoglobin | Boolean (0/1) | Categorical |
| **CPK** | Level of the CPK enzyme in the blood | mcg/L | Continuous |
| **Diabetes** | If the patient has diabetes | Boolean (0/1) | Categorical |
| **Ejection Fraction**| Percentage of blood leaving the heart at each contraction | Percentage | Continuous |
| **High Blood Pressure**| If a patient has hypertension | Boolean (0/1) | Categorical |
| **Platelets** | Platelets in the blood | kiloplatelets/mL | Continuous |
| **Serum Creatinine**| Level of creatinine in the blood | mg/dL | Continuous |
| **Serum Sodium** | Level of sodium in the blood | mEq/L | Continuous |
| **Gender** | Woman (0) or man (1) | Binary | Categorical |
| **Smoking** | If the patient smokes | Boolean (0/1) | Categorical |
| **Time** | Follow-up period | Days | Continuous |
| **DEATH_EVENT** | If the patient died during follow-up (Target) | Boolean (0/1) | Categorical |

## 📈 Exploratory Data Analysis (EDA)

The EDA revealed key insights into the data distribution and relationships between features and the target variable.

*   **Outlier Analysis:** Continuous variables like `creatinine`, `platelets`, and `CPK` showed significant outliers. However, after careful domain-specific analysis, these were retained as they represent clinically valid, albeit extreme, patient conditions that are crucial for prediction. For example, creatinine levels above 5.0 mg/dL, though statistically outliers, denote severe kidney failure and are highly relevant.
*   **Correlations:**
    *   **Age:** Higher age is correlated with a greater chance of death.
    *   **Ejection Fraction:** Values below 30% or above 75% show a significant correlation with heart failure.
    *   **Serum Creatinine:** Levels above 5.0 mg/dL indicate a high risk of heart failure.
    *   **Time:** A shorter follow-up period (`time`) is strongly associated with mortality, as high-risk patients were monitored for shorter durations.
    *   **Platelets:** No significant relationship was found with the death event.


## ⚙️ Methodology

The project followed a structured approach from data cleaning to model deployment.

### Data Pre-processing
The dataset was clean, with **no missing values**. A multicollinearity check was performed using a correlation matrix, which confirmed that all predictor correlations were below 0.25, indicating no significant multicollinearity issues.

### Feature Selection
The **Best Subset Method** was used to identify the most predictive combination of features. Models were evaluated based on BIC (Bayesian Information Criterion), R², and Adjusted-R².
*   The model with the lowest **BIC** contained **4 features**.
*   The model with the highest **Adjusted R²** contained **6 features**.

Given the small dataset size, BIC is preferred as it heavily penalizes model complexity, reducing the risk of overfitting. Performance evaluation confirmed that the 4-variable subset yielded the best results.

The **top 4 selected features** for the final model were:
1.  **Time**
2.  **Ejection Fraction**
3.  **Serum Creatinine**
4.  **Age**

### Model Selection
Three models were evaluated for the classification task:
1.  **Logistic Regression**
2.  **Decision Tree**
3.  **Random Forest**

**Bootstrapping** was used for validation due to the small dataset size. Across multiple iterations, Random Forest consistently achieved the highest accuracy.

| Model | Accuracy (Bootstrap Avg.) |
| :--- | :--- |
| Logistic Regression| ~83.7% |
| Decision Tree | ~86.4% |
| **Random Forest** | **~94.1%** |

## 🎯 Final Model & Results

The final predictive model is a **Random Forest classifier**, built using the four selected features.

### Hyperparameter Tuning
The model was fine-tuned for the number of trees, variables per split (`mtry`), and node size to optimize performance. The best results were achieved with `mtry=1` and `100 trees`.

### Performance
After tuning, the final Random Forest model achieved an **accuracy of 81.33%** on the held-out test data.

### Feature Importance
The model confirmed the importance of the selected features, ranked as follows:
1.  **Time** (Follow-up period)
2.  **Serum Creatinine**
3.  **Ejection Fraction**
4.  **Age**



## ✅ Conclusion

This study successfully developed a robust machine learning model for predicting heart failure mortality. The **Random Forest model**, using only four clinical markers (`time`, `serum_creatinine`, `ejection_fraction`, and `age`), demonstrated strong predictive power with an **81.33% accuracy**.

The findings underscore the significance of these markers in heart failure prognosis and highlight the potential of data-driven approaches to aid in early risk assessment, contributing to better clinical outcomes in cardiovascular health.

## 🚀 Future Scope

While this study provides valuable insights, future work could explore the following areas:
*   **Advanced Models:** Incorporate deep learning algorithms to uncover more complex patterns.
*   **Longitudinal Data:** Use longitudinal studies to track patient progression over longer periods.
*   **Genomic Data:** Integrate genetic and genomic data for personalized risk assessments.
*   **Real-time Monitoring:** Leverage data from wearable devices to build dynamic and more precise predictive models.

[📄 Download Full Report (PDF)](heart_failure_report.pdf)

## ✍️ Author 

This project was conducted and documented by **Awnish Shankar**.
