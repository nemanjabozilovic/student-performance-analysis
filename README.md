# Student Performance Prediction using Machine Learning

## Project Overview

This project focuses on predicting the final student grade (**G3**) using machine learning techniques.  
The dataset contains information about students’ academic performance, personal background, and behavioral factors.

The goal of the project is to build, evaluate, and interpret regression models that can accurately predict the final grade based on available features, while also providing insights into the factors that most strongly influence student performance.

---

## Problem Definition

### Why Regression Is the Default Choice

In this dataset, the target variable **G3** represents a numerical value ranging from **0 to 20**, corresponding to the final student grade.  
Since the objective is to predict an exact numerical outcome, the problem is naturally formulated as a **supervised regression task**.

**Example:**  
Predict the final grade (G3) based on student characteristics and previous academic performance.

Although regression is the primary approach, the dataset also allows alternative formulations by redefining the target variable.

---

### Binary Classification

- **pass** (G3 ≥ 10)  
- **fail** (G3 < 10)

**Task:** Predict whether a student will pass or fail.

---

### Multiclass Classification

- **low** (0–9)  
- **medium** (10–14)  
- **high** (15–20)

**Task:** Predict the grade category of a student.

---

### Problem Definition Used in This Project

In this project, the problem is primarily approached as a **regression task**, where the goal is to predict the final student grade (**G3**).  
Alternative problem formulations are acknowledged but not implemented.

---

## Exploratory Data Analysis (EDA)

Exploratory Data Analysis (EDA) represents the initial step in the machine learning workflow and is used to understand the structure and characteristics of the dataset before model training.

The dataset consists of **395 instances** and **33 features**, with no missing values detected. Both numerical and categorical variables are present, which requires different preprocessing strategies in later stages.

Descriptive statistics were used to examine numerical features, including mean values, standard deviations, minimum and maximum values, and quartile distributions. This provided insight into value ranges and potential outliers.

Correlation analysis revealed a strong relationship between the final grade (**G3**) and previous grades (**G1** and **G2**), indicating that earlier academic performance is a key factor in predicting final outcomes. Additional variables such as absences and study time showed a moderate influence on student performance.

Categorical features were analyzed in terms of cardinality. Most categorical variables have a small number of unique values, making them suitable for one-hot encoding.

Overall, the EDA confirmed that the dataset is clean, consistent, and well-prepared for preprocessing and model training.

---

## Feature Preprocessing

Before training the models, preprocessing steps were defined to appropriately prepare the data.

Since the dataset contains both numerical and categorical features, different preprocessing techniques were applied.

### Numerical Features

- Standardized using standardization (mean = 0, standard deviation = 1)
- Ensures all numerical variables are on the same scale
- Prevents features with larger numeric ranges from dominating the model

### Categorical Features

- Transformed using **one-hot encoding**
- Converted into binary numerical features
- The first category was dropped to avoid multicollinearity
- Unknown categories in the test set were safely ignored

All preprocessing steps were combined into a single preprocessing pipeline, ensuring that transformations are applied consistently and only learned from the training data, preventing data leakage.

---

## Model Training and Evaluation

After preprocessing, models were trained using a pipeline that combines preprocessing and model fitting into a single workflow.

---

### Baseline Model: Linear Regression

Linear Regression was used as a baseline model due to its simplicity and interpretability.  
The model was trained on the training set and evaluated on a separate test set to simulate real-world prediction.

Model performance was evaluated using standard regression metrics:

- **MAE (Mean Absolute Error)**
- **MSE (Mean Squared Error)**
- **RMSE (Root Mean Squared Error)**
- **R² (Coefficient of Determination)**

The baseline model achieved solid performance, explaining a significant portion of the variance in final grades.

---

## Feature Importance – Linear Regression

The coefficients of the linear regression model were analyzed to interpret the influence of individual features on the predicted final grade.

- Positive coefficients indicate features that increase the predicted grade
- Negative coefficients indicate a decreasing effect
- The magnitude of the coefficient reflects the strength of the influence

The analysis showed that previous grades (**G1** and especially **G2**) are the strongest predictors of the final grade.  
Factors such as absences and previous failures have a negative impact, while academic support and future educational aspirations have a positive influence.

This analysis confirms that academic history plays a dominant role, while social and behavioral factors have secondary but measurable effects.

---

## Model Comparison – Random Forest Regression

To improve performance and capture nonlinear relationships, a **Random Forest Regressor** was implemented and compared to the baseline linear regression model.

Random Forest is an ensemble method that combines multiple decision trees trained on different subsets of data and features.  
The final prediction is obtained by averaging the predictions of all trees, resulting in a more robust and stable model.

The Random Forest model was trained using the same preprocessing pipeline and evaluated with the same metrics, ensuring a fair comparison.

### Results

Random Forest achieved:

- Lower MAE and RMSE  
- Higher R² score  

This indicates improved predictive performance and better handling of nonlinear relationships in the data.

---

## Feature Importance – Random Forest

Feature importance analysis from the Random Forest model revealed that previous academic performance remains the dominant factor, with **G2** being the most influential feature by a large margin.

Secondary factors such as absences, family-related reasons, and age also contributed to predictions, while social and behavioral variables had a smaller impact.

These results align with the linear regression analysis but additionally highlight the importance of nonlinear interactions captured by the Random Forest model.

---

## Error Analysis

Error analysis was conducted to better understand how the model behaves beyond aggregate performance metrics.

Residuals (differences between actual and predicted grades) were generally centered around zero, indicating no strong systematic overestimation or underestimation.

The model performed best for mid-range grades, while larger errors were observed for very low and very high grades.  
This behavior is common in real-world educational data, where extreme cases are influenced by unobserved factors.

Overall, the model demonstrates stable and consistent behavior, with limitations primarily at the extremes of the target distribution.

---

## Cross-Validation

To obtain a more reliable estimate of model performance, **k-fold cross-validation** was applied using a 5-fold strategy.

The model was trained and evaluated multiple times on different data splits, reducing dependence on a single train-test split.  
Mean Absolute Error (MAE) was used as the evaluation metric.

Results showed low variability across folds, indicating good generalization and robustness of the Random Forest model.

---

## Final Conclusion

This project implemented a complete machine learning workflow for predicting student final grades, including data exploration, preprocessing, model training, evaluation, interpretation, and comparison.

The analysis confirmed that previous academic performance is the strongest predictor of final grades, while behavioral and social factors play a secondary role.

Random Forest Regression outperformed the baseline linear regression model, demonstrating better accuracy and generalization due to its ability to capture nonlinear relationships.

While the model shows strong performance, it is important to note that student success is influenced by many factors not present in the dataset, such as motivation, teaching quality, and socio-economic conditions.
