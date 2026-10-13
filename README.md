# Diabetes-Prediction and Analysis
A beginner-friendly machine learning project that explores a diabetes dataset and builds a model to predict whether a patient has diabetes from basic health measurements.

###Overview

- **Goal:** Find which health measurements relate most to diabetes, and predict diabetes from them.
- **Dataset:** Diabetes dataset from Kaggle (768 patients, 8 features, 1 target).
- **Tools:** Python, Jupyter Notebook, pandas, seaborn, matplotlib, scikit-learn.
- **Final result:** 76.7% test accuracy, with 66% recall for diabetes cases.

## Dataset

| Column | Description |
|---|---|
| Pregnancies | Number of pregnancies |
| Glucose | Plasma glucose concentration |
| BloodPressure | Diastolic blood pressure (mm Hg) |
| SkinThickness | Triceps skin fold thickness (mm) |
| Insulin | 2-hour serum insulin |
| BMI | Body mass index |
| DiabetesPedigreeFunction | Family history score |
| Age | Age in years |
| **Outcome** | **0 = no diabetes, 1 = diabetes** |

## Project Workflow

1. **Load and inspect** the data with pandas.
2. **Clean the data.** Zeros in Glucose, BloodPressure, SkinThickness, Insulin and BMI are impossible values, so they were treated as missing and replaced with the column median.
3. **Explore** with box plots and a correlation heatmap.
4. **Split** the data into 70% training, 15% validation and 15% testing (stratified).
5. **Scale** the features with `StandardScaler` (fitted on training data only).
6. **Train and compare models** on the validation set.
7. **Evaluate** the chosen model once on the test set.

## Key Findings

- **Glucose** has the strongest link to diabetes (correlation 0.49), followed by **BMI** (0.31).
- Blood pressure and insulin are weak predictors on their own.
- People with diabetes have clearly higher glucose levels, and the two groups barely overlap.
- No single feature predicts diabetes alone, so combining features works better.

## Model Results

Validation set (115 patients):

| Model | Accuracy | Diabetes recall | Diabetes f1 |
|---|---|---|---|
| Logistic Regression | 0.72 | 0.55 | 0.58 |
| Logistic Regression (balanced) | 0.74 | 0.75 | 0.67 |
| Random Forest (balanced) | 0.76 | 0.62 | 0.64 |

**Chosen model:** Logistic Regression with `class_weight="balanced"`. In a screening setting, missing a real case is costlier than a false alarm, so recall for diabetes mattered most.

Final test set (116 patients):

| Class | Precision | Recall | f1 |
|---|---|---|---|
| 0 (no diabetes) | 0.82 | 0.83 | 0.82 |
| 1 (diabetes) | 0.68 | 0.66 | 0.67 |
| **Accuracy** | | | **0.77** |

## How to Run

1. Clone this repository.
2. Install the requirements:
   ```bash
   pip install pandas numpy seaborn matplotlib scikit-learn jupyter
   ```
3. Put the dataset CSV in the same folder as the notebook.
4. Open the notebook:
   ```bash
   jupyter notebook diabetes_analysis.ipynb
   ```
5. Click **Kernel > Restart & Run All** so the cells run in order.

## Limitations

- Small dataset (768 rows), so results shift a little with each split.
- Missing values were filled with medians, which reduces natural variation. The medians were also computed before the split, which lets a small amount of information from the validation and test sets leak into training. Doing the imputation after splitting would be stricter.
- Recall for diabetes (66% on test) can still be improved.
- This project is for learning only and must not be used for real medical decisions.



## Author
Kikelomo
https://github.com/Aro-Kike


Your Name | [GitHub](https://github.com/your-username)
