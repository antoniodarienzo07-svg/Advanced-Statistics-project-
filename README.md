# Advanced Statistics for Finance - S&P 500 Market Analysis

This repository contains the project developed for the **Advanced Statistics for Finance** course (June 2025) at Sapienza University of Rome. The project focuses on data cleaning, descriptive statistics, variable selection techniques and predictive modeling applied to the weekly returns of the S&P 500 stock market index.

## Project Overview
The main objective of this study is to analyze the predictive power of historical financial variables (past returns and trading volumes) on current market performance. The project compares traditional parametric approaches (Multiple Linear Regression with Stepwise Selection and Cross-Validation) against a non-parametric machine learning algorithm ($k$-Nearest Neighbors).

The analysis is conducted entirely in **R** utilizing the `Weekly` dataset from the `ISLR2` library, which contains 1,089 weekly observations from 1990 to 2010.

## Key Features & Methodology

1. **Data Cleaning & Preprocessing:**
   * Automated missing data detection (`na.omit`). The dataset was verified to be 100% complete (0% missing values).
2. **Exploratory Data Analysis (EDA):**
   * Statistical analysis of weekly returns (`Today` variable) evaluating Mean, Median, Standard Deviation, Skewness, and Kurtosis.
   * Visual analysis via detailed distribution histograms showing typical financial stylized facts (heavy tails / leptokurtic distribution).
3. **Linear Regression & Variable Selection:**
   * Implementation of a full Multiple Linear Regression model avoiding data leakage (excluding the `Direction` factor).
   * Feature selection via **Forward Stepwise Selection** and **Backward Stepwise Selection** minimized through the **Bayesian Information Criterion (BIC)**.
   * Model validation using **10-fold Cross-Validation** to evaluate generalization capabilities and mitigate overfitting.
4. **Classification via $k$-Nearest Neighbors ($k$-NN):**
   * Market direction prediction (`Up` vs `Down`) using lagged returns (`Lag1` to `Lag5`) and trading `Volume`.
   * Data split into Training (70%) and Testing (30%) sets.
   * Model performance evaluation via Confusion Matrix and Accuracy metrics.

## Key Findings
* **Market Efficiency:** The linear regression model confirms the highly noisy nature of stock returns (Adjusted $R^2 < 1\%$). A weak mean-reversion effect was detected through the statistical significance of `Lag1` and `Lag3`.
* **Model Selection:** Stepwise Selection and Cross-Validation both favored a parsimonious model featuring only `Lag1` as a predictor, prioritizing variance reduction and generalization over complexity.
* **$k$-NN Performance:** The $k$-NN classifier ($k=5$) achieved an accuracy of **56.3%** on the test set. While modest, this represents a statistically relevant edge over a random 50% guess in a notoriously random-walk environment.

## Libraries Used
The following R packages are required to run the code:
```R
library(ISLR2)   # Dataset source
library(e1071)   # Skewness and Kurtosis calculation
library(leaps)   # Subset selection (Forward/Backward)
library(boot)    # Cross-validation tools
library(class)   # k-NN algorithm
library(caret)   # Data splitting and advanced CV evaluation


