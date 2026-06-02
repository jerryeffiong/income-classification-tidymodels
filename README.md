# Income Classification with Tidymodels

## Project Objective
This project features a machine-learning workflow designed to predict whether an adult in the U.S. earns more than $50K per year. The primary aim is to understand the drivers of higher earnings through data provenance, cleaning, modeling, evaluation, and interpretability. The success criteria for this project included achieving a ROC AUC above 0.80 on a held-out test set and delivering a transparent model that can be explained to non-technical stakeholders.

## Dataset Overview
* **Source:** OpenML Adult Census Income dataset containing 48,842 records and 15 features.
* **Data Types:** Mixed numeric and categorical predictors including age, education, and occupation.
* **Target Variable:** Income bracket, classified as either `<=50K` or `>50K`.

## Methodology & Preprocessing
The data preparation pipeline was built using the `recipes` package in R. Key preprocessing steps included:
* Converting '?' placeholders to 'Unknown' categories.
* Grouping rare categorical levels using `step_other()`.
* Applying one-hot encoding to factors and normalizing numeric features with `step_normalize()`.
* Removing zero-variance and highly correlated predictors to reduce noise.
* Implementing SMOTE and downsampling to handle class imbalance.

## Modeling Pipeline
Three distinct algorithms were trained and evaluated using the `tidymodels` framework:
1.  **Regularized Logistic Regression** (`glmnet`)
2.  **Radial Basis SVM** (`kernlab`)
3.  **Random Forest Ensemble** (`ranger`)

Hyperparameter tuning was conducted using 5-fold stratified cross-validation on the training set, optimizing for ROC AUC and accuracy.

## Results & Performance
The models were evaluated on a held-out test set, with Random Forest achieving the highest performance on the primary target metric:
* **Random Forest:** Accuracy 0.819, ROC AUC 0.888
* **Logistic Regression:** Accuracy 0.788, ROC AUC 0.888
* **Radial Basis SVM:** Accuracy 0.780, ROC AUC 0.884

## Model Interpretability
To ensure the model's logic was transparent and actionable, both global and local interpretability techniques were applied.

**Global Interpretability:**
* Permutation importance methods consistently identified Marital status, Education-num, Age, and Hours-per-week as the strongest predictors across all three models.
* Partial Dependence Plots (PDP) revealed that earnings probability peaks at approximately age 51 and experiences a slight decline before plateauing.

**Local Interpretability:**
* LIME (Local Interpretable Model-Agnostic Explanations) was deployed to analyze individual test observations.
* Local explanations confirmed that education, marital status, age, and work hours explained the majority of prediction variance across diverse individual cases.

## Tech Stack
* **Language:** R
* **Core Libraries:** `tidymodels`, `recipes`, `rsample`, `tune`, `workflows`, `ggplot2`
* **Algorithms:** `glmnet`, `kernlab`, `ranger`
* **Interpretability:** `pdp`, `lime`, `vip`
