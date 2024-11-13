# Diabetes Prediction Model

This project aims to build a machine learning model that can predict diabetes onset based on diagnostic measures. The dataset used includes various health indicators for female patients of Pima Native American heritage who are at least 21 years old.

---

## Table of Contents
1. [About the Project](#about-the-project)
   - [Goals](#goals)
   - [Background](#background)
   - [Project Outline](#project-outline)
   - [Acknowledgments](#acknowledgments)
2. [Data Dictionary](#data-dictionary)
   - [Original Dataframe](#original-dataframe)
   - [Added Features](#added-features)
3. [Initial Thoughts & Hypotheses](#initial-thoughts--hypotheses)
   - [Thoughts](#thoughts)
   - [Hypotheses](#hypotheses)
4. [Project Steps](#project-steps)
   - [Acquire](#acquire)
   - [Prepare](#prepare)
   - [Explore](#explore)
   - [Model](#model)
   - [Conclusions](#conclusions)
5. [How to Reproduce the Files](#how-to-reproduce-the-files)

---

## About the Project

### Goals
The main goal of this project is to develop a machine learning model that can predict whether a patient has diabetes based on diagnostic data like BMI and age.

### Background
Early detection of diabetes is critical in preventing severe complications, such as cardiovascular diseases, blindness, kidney failure, and more. This project utilizes diagnostic data to aid in early detection, helping individuals who may not show symptoms but are at risk.

### Project Outline
1. **README**: Project description and outline.
2. **diabetes_analysis.ipynb**: The complete data science pipeline.
3. **Prepare.py**: Script with functions for dataset preprocessing.

### Acknowledgments
Data obtained from the UCI Machine Learning Repository, with contributions by:
- Smith, J.W., Everhart, J.E., Dickson, W.C., Knowler, W.C., & Johannes, R.S. (1988). *Proceedings of the Symposium on Computer Applications and Medical Care*, IEEE Computer Society Press.

---

## Data Dictionary

### Original Dataframe
| Feature                | Description                                          |
|------------------------|------------------------------------------------------|
| Outcome                | Binary class (0 = non-diabetic, 1 = diabetic)        |
| Pregnancies            | Number of times pregnant                            |
| Glucose                | Plasma glucose concentration (2-hour oral glucose test) |
| Blood Pressure         | Diastolic blood pressure (mm Hg)                    |
| Skin Thickness         | Triceps skin fold thickness (mm)                    |
| Insulin                | 2-hour serum insulin (mu U/ml)                      |
| BMI                    | Body mass index: weight in kg/(height in m)^2       |
| Diabetes Pedigree Function | Measure of genetic influence                 |
| Age                    | Age of patient in years                             |

### Added Features
| Feature Name            | Description                                         |
|-------------------------|-----------------------------------------------------|
| age_bins                | Age split into 4 bins (1 through 4)                 |
| bmi_bins                | BMI split into 3 bins (1 through 3)                 |
| bp_bins                 | Blood pressure split into 3 bins (1 through 3)      |
| high_bmi_bp             | Boolean indicating high BMI and Blood Pressure      |
| age_bmi_cluster         | Cluster based on Age and BMI                        |
| pregnancy_cluster       | Cluster based on number of pregnancies              |
| insulin_and_glucose_cluster | Cluster using Insulin and Glucose data         |

---

## Initial Thoughts & Hypotheses

### Thoughts
Numerous studies indicate that health factors like higher BMI are significant risk indicators for diabetes. This project aims to analyze whether these factors correlate with diabetes within this dataset.

### Hypotheses
1. **Age vs. Outcome**
   - Null: Age does not influence diabetes diagnosis.
   - Alternative: Higher age correlates with higher diabetes diagnosis.
   - Test: Pearson correlation (Result: Rejected null, correlation coefficient = 0.24).

2. **BMI vs. Outcome**
   - Null: BMI does not significantly affect diabetes diagnosis.
   - Alternative: Higher BMI correlates with higher diabetes incidence.
   - Test: One-sample T-test (Result: Rejected null, t-value = 3.0).

3. **Blood Pressure vs. Outcome**
   - Null: Blood pressure does not influence diabetes diagnosis.
   - Alternative: Higher blood pressure correlates with diabetes.
   - Test: One-sample T-test (Result: Failed to reject null).

---

## Project Steps

### Acquire
Data was sourced from Kaggle, with 768 observations and nine features. Null values were replaced with zeros in specific features.

### Prepare
Preprocessing steps included:
- Replacing zero values with feature means.
- Binning and clustering features using `pandas.qcut` and `KMeans`.
- Splitting data into training, validation, and test datasets (70-20-10 split).
- Scaling features with `MinMaxScaler`.

### Explore
Exploratory data analysis included:
- Comparing independent features with the Outcome variable.
- Analyzing relationships among independent features.
- Examining cluster subgroups against the Outcome variable.

### Model
#### Baseline Model
A baseline model was created predicting all outcomes as non-diabetic, resulting in a 66% accuracy on training data (0% recall rate for diabetic cases).

#### Models Tested
1. Logistic Regression Model
2. Decision Tree Model
3. Random Forest Model
4. KNN Model

#### Final Model: Random Forest
The Random Forest model was selected for its balanced performance on accuracy, recall, and precision, with particular emphasis on recall for diabetic cases.

| Model          | Dataset  | Accuracy | Recall (Positive) | Precision (Positive) |
|----------------|----------|----------|--------------------|-----------------------|
| Random Forest  | Train    | 86%      | 74%               | 83%                   |
|                | Validate | 78%      | 62%               | 72%                   |
|                | Test     | 74%      | 60%               | 69%                   |

Random Forest aggregates multiple decision trees, with each using random feature subsets. Final predictions are based on the majority vote across trees.

### Conclusions
- **Key Findings**: Glucose levels are the most influential predictor, followed by age and BMI.
- **Next Steps**: Improve model performance by creating additional cluster subgroups.

The final Random Forest model demonstrates high recall, making it suitable for early diabetes detection and aiding in the prevention of complications.

---

## How to Reproduce the Files

1. Review the `README.md` file for an overview of the project.
2. Download the following files: `diabetes_analysis.ipynb`, `Prepare.py`, and `diabetes.csv` dataset.
3. Open and run the `diabetes_analysis.ipynb` notebook to execute the full analysis pipeline.

--- 

This project provides a robust approach to early diabetes diagnosis through machine learning.
