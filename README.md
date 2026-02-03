# Student Performance Prediction Using Machine Learning

## Project Overview

This project focuses on predicting the final student grade (G3) using supervised machine learning techniques.  
The dataset contains information related to students’ academic history, personal background, and behavioral characteristics.

The main objective of the project is to develop regression models capable of predicting the final grade with good accuracy, to evaluate their performance using standard metrics, and to analyze which factors have the strongest influence on student performance.

The project follows a complete machine learning workflow, including exploratory data analysis, preprocessing, model training, evaluation, interpretation, model comparison, and final model selection.

---

## Problem Definition

The target variable G3 represents the final student grade and takes continuous numerical values in the range from 0 to 20.  
Since the task involves predicting an exact numerical outcome based on a set of input features, the problem is formulated as a supervised regression problem.

Although the dataset could also be adapted for classification tasks by grouping grades into categories (such as pass/fail or performance levels), this project focuses on regression in order to preserve the full numerical information contained in the final grade.

---

## Exploratory Data Analysis (EDA)

Exploratory Data Analysis (EDA) was conducted as the first step to understand the structure and characteristics of the dataset before applying machine learning models.

The dataset consists of 395 instances and 33 features, and no missing values were detected. This indicates that no additional data cleaning or imputation was required.

Both numerical and categorical variables are present, which implies the need for different preprocessing strategies. Descriptive statistics were used to summarize numerical features, including mean values, standard deviations, minimum and maximum values, and quartile distributions. This provided insight into value ranges and variability across features.

Correlation analysis showed a strong relationship between the final grade (G3) and previous academic performance indicators (G1 and G2). This suggests that earlier grades are strong predictors of final outcomes. Additional variables such as the number of absences and study time showed a moderate influence on student performance.

Categorical features were analyzed based on their number of unique values. Most categorical variables have low cardinality, making them suitable for one-hot encoding.

Overall, the EDA confirmed that the dataset is clean, consistent, and appropriate for further preprocessing and model training.

---

## Feature Preprocessing

Before training the models, preprocessing steps were defined to transform the data into a format suitable for machine learning algorithms.

### Numerical Features

Numerical features were standardized using standardization, which transforms each feature to have a mean of zero and a standard deviation of one.  
This ensures that all numerical variables are on a comparable scale and prevents features with larger numeric ranges from dominating the learning process.

### Categorical Features

Categorical features were transformed using OneHotEncoder. One-hot encoding converts categorical values into binary numerical features, where each category is represented by a separate binary column.

One category per feature is dropped to avoid multicollinearity, and unseen categories in the test set are safely ignored.

All preprocessing steps were combined into a single preprocessing pipeline, ensuring that transformations are learned only from the training data and applied consistently, thus preventing data leakage.

---

## Model Training and Evaluation

The dataset was split into training and test sets to simulate real-world prediction scenarios.  
Models were trained using pipelines that integrate preprocessing and model fitting into a single workflow.

---

## Evaluation Metrics

Model performance was evaluated using the following regression metrics:

- **Mean Absolute Error (MAE)**  
  Represents the average absolute prediction error, expressed in the same units as the target variable.

- **Root Mean Squared Error (RMSE)**  
  Penalizes larger errors more heavily and is sensitive to larger deviations.

- **Coefficient of Determination (R²)**  
  Measures the proportion of variance in the target variable explained by the model.

---

## Baseline Model: Linear Regression

Linear Regression was used as a baseline model due to its simplicity and interpretability.

**Test set performance:**

- MAE = 1.65  
- RMSE = 2.38  
- R² = 0.72  

These results indicate that the model predicts the final grade with an average absolute error of approximately 1.6 grade points.  
The RMSE value shows that in cases of larger errors, predictions may deviate by 2–3 grade points.  
The R² score of 0.72 means that the model explains 72% of the variance in final grades.

While the model provides reasonable performance, it assumes linear relationships between features and the target variable, which limits its ability to capture more complex patterns.

---

## Model Interpretation: Linear Regression Coefficients

The coefficients of the Linear Regression model were analyzed to interpret the influence of individual features.

The analysis shows that previous academic performance, particularly G2, has the strongest positive impact on the final grade.  
G1 also contributes significantly, confirming the importance of academic continuity.

Variables such as absences and previous failures have a negative effect, while academic support and plans for higher education have a positive influence.

These findings indicate that academic factors dominate, while social and behavioral variables play a secondary but measurable role.

---

## Model Comparison: Random Forest Regression

To capture nonlinear relationships and feature interactions, a Random Forest Regressor was implemented and compared with the baseline model.

Random Forest is an ensemble method that combines predictions from multiple decision trees trained on different subsets of data and features.  
The final prediction is obtained by averaging predictions from all trees, which improves robustness and reduces overfitting.

**Random Forest test set performance:**

- MAE = 1.18  
- RMSE = 1.98  
- R² = 0.81  

Compared to Linear Regression, Random Forest reduces the average absolute error by approximately 0.47 grade points, lowers RMSE by 0.40, and increases the explained variance by 9 percentage points.

---

## Discussion and Model Evaluation

The comparison between Linear Regression and Random Forest Regression clearly shows that Random Forest provides superior performance across all evaluation metrics.

Linear Regression explains 72% of the variance in final grades, while Random Forest increases this value to 81%.  
The reduction in MAE from 1.65 to 1.18 indicates a substantial improvement in prediction accuracy.  
Similarly, the lower RMSE demonstrates better handling of larger prediction errors.

These results suggest that student performance is influenced by nonlinear relationships and interactions between variables, which are better captured by the Random Forest model.

While Linear Regression remains valuable due to its interpretability, Random Forest offers a better balance between accuracy and robustness for this dataset.

---

## Error Analysis

Error analysis showed that prediction residuals are generally centered around zero, indicating no strong systematic bias.

The model performs best for mid-range grades, while larger errors occur for very low and very high grades.  
This behavior is common in educational datasets, where extreme outcomes are often influenced by factors not present in the data.

---

## Cross-Validation

A 5-fold cross-validation procedure was applied to assess model stability.  
The evaluation showed low variability in performance across folds, confirming that the Random Forest model generalizes well and is not overly dependent on a single train-test split.

---

## Final Conclusion

This project demonstrates a complete machine learning workflow for predicting student final grades.

Exploratory analysis confirmed the importance of academic history, particularly previous grades, as the strongest predictors of final outcomes.

Linear Regression provided a solid and interpretable baseline, achieving R² = 0.72, while Random Forest Regression significantly improved performance with R² = 0.81 and lower prediction errors.

Based on quantitative evaluation and model comparison, Random Forest Regression is the most suitable model for this dataset, as it achieves higher accuracy, better generalization, and more robust predictions.

Future work may include hyperparameter tuning, feature engineering, or the application of advanced ensemble and boosting methods.  
Despite strong results, it should be noted that student performance is influenced by many real-world factors not captured in the dataset, such as motivation, teaching quality, and socio-economic conditions.
