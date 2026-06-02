# Income Classification with Tidymodels

## Project Objective
[cite_start]This project features a machine-learning workflow designed to predict whether an adult in the U.S. earns more than $50K per year[cite: 147]. [cite_start]The primary aim is to understand the socio-economic drivers of higher earnings through data provenance, cleaning, modeling, evaluation, and interpretability[cite: 148]. [cite_start]The success criteria for this project included achieving a ROC AUC above 0.80 on a held-out test set and delivering a transparent model that can be explained to non-technical stakeholders[cite: 149].

## Dataset Overview
* [cite_start]**Source:** OpenML Adult Census Income dataset containing 48,842 records and 15 features[cite: 151].
* [cite_start]**Data Types:** Mixed numeric and categorical predictors including age, education, and occupation[cite: 152, 153].
* [cite_start]**Target Variable:** Income bracket, classified as either `<=50K` or `>50K`[cite: 154].

## Methodology & Preprocessing
[cite_start]The data preparation pipeline was built using the `recipes` package in R[cite: 102]. Key preprocessing steps included:
* [cite_start]Converting '?' placeholders to 'Unknown' categories[cite: 211, 212, 213].
* [cite_start]Grouping rare categorical levels using `step_other()`[cite: 214, 215].
* [cite_start]Applying one-hot encoding to factors and normalizing numeric features with `step_normalize()`[cite: 216, 217, 218, 219].
* [cite_start]Removing zero-variance and highly correlated predictors to reduce noise[cite: 220, 221].
* [cite_start]Implementing SMOTE (Synthetic Minority Over-sampling Technique) and downsampling to handle class imbalance[cite: 126].

## Modeling Pipeline
[cite_start]Three distinct algorithms were trained and evaluated using the `tidymodels` framework[cite: 264]:
1.  [cite_start]**Regularized Logistic Regression** (`glmnet`) [cite: 261]
2.  [cite_start]**Radial Basis SVM** (`kernlab`) [cite: 262]
3.  [cite_start]**Random Forest Ensemble** (`ranger`) [cite: 263]

[cite_start]Hyperparameter tuning was conducted using 5-fold stratified cross-validation on the training set, optimizing for ROC AUC and accuracy[cite: 273, 274, 276].

## Results & Performance
The models were evaluated on a held-out test set. [cite_start]The Random Forest model achieved the highest performance on the primary target metric[cite: 283]:
* [cite_start]**Random Forest:** Accuracy 0.819, ROC AUC 0.888 [cite: 280, 482]
* [cite_start]**Logistic Regression:** Accuracy 0.788, ROC AUC 0.888 [cite: 281]
* [cite_start]**Radial Basis SVM:** Accuracy 0.780, ROC AUC 0.884 [cite: 282]

## Model Interpretability
To ensure the model's logic was transparent and actionable, both global and local interpretability techniques were applied.

**Global Interpretability:**
* [cite_start]Permutation importance methods consistently identified Marital status, Education-num, Age, and Hours-per-week as the strongest predictors across all three models[cite: 483, 484].
* [cite_start]Partial Dependence Plots (PDP) revealed that earnings probability peaks at approximately age 51 and experiences a slight decline before plateauing[cite: 478].

**Local Interpretability:**
* [cite_start]LIME (Local Interpretable Model-Agnostic Explanations) was deployed to analyze individual test observations[cite: 471, 479].
* [cite_start]Local explanations confirmed that education, marital status, age, and work hours explained the majority of prediction variance across diverse individual cases[cite: 479].

## Tech Stack
* **Language:** R
* [cite_start]**Core Libraries:** `tidymodels`, `recipes`, `rsample`, `tune`, `workflows`, `ggplot2` [cite: 102]
* [cite_start]**Algorithms:** `glmnet`, `kernlab`, `ranger` [cite: 126, 129, 132]
* [cite_start]**Interpretability:** `pdp`, `lime`, `vip` [cite: 102]
