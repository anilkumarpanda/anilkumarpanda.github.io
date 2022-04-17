---
layout: post
title: Error Analysis for Tabular Data - Part 2
---

In this post we will explore the Residual Analysis method for model debugging.

I will adapt the Residual analysis method from [this](https://nbviewer.org/github/jphall663/GWU_rml/blob/master/lecture_5.ipynb) repo.

** Residual Analysis **

Residuals refer to the difference between the recorded value of a dependent variable and the predicted value of a dependent variable for every row in a data set. Plotting the residual values against the predicted values is a time-honoured model assessment technique and a great way to see all your modelling results in two dimensions.

Analysing residuals can provide us with great insights about the model behaviour both on a global level and also on a feature level.It can reveal insights such about the data points for which our model is making mistakes.

I will cover explore two methods for residual analyis:

1. Residual analyis on global & feature level
2. Modelling of residuals

For demonstration purposes, I will explore the model created on Lending Club data.The data is available on [Kaggle](https://www.kaggle.com/lendingclub/loan-data).The task is to create a binary classification model, to predict loan defaults at the time of loan origination.Such models are also known as Application models/score models.

I created a LightGBM model using the following features. The explaination of the features can be found in the data dictionary.

```
    "emp_length",
    "addr_state",
    "revol_util",
    "revol_bal",
    "term",
    "num_actv_bc_tl",
    "total_acc",
    "application_type",
    "purpose",
    "grade",
    'dti',
    "home_ownership",
    "annual_inc",
    "num_tl_90g_dpd_24m"
```
The LGB model has **decent** performance on the test set, with an AUC of 0.68 on test set. The details of the model can be found below
![lending clun model](../images/ra_lc_model_scorecard.png)

Now that we have a model, lets start with the residual analysis.

## Residual Analysis

### Residual Analysis on Global Level

Here I will explore the model behaviour on the global level. The plot show the model residuals against the actual values(classes) of the dependent variable.

![global residuals](../images/ra_global.png)

We see that indeed the model is making mistakes for quite a few of the data points. Especially for `loan_status==1`.
This raises a few interesting questions :

* Who are these customers?
* Why is the model so wrong about them?
* Are they somehow exerting undue influence on other predictions?

To answer these questions we can also conduct residual analysis on the feature level.

### Residual Analysis on Feature Level

In this method, we will plot the residuals against the predicted values of the dependent variable for each feature(or atleast a few important features).
In our case, lets take the example of the `grade` feature.

Intuitively,higher the grade, less chances of default. However on closer analysis we see that the model is making mistakes for the customers who have a grade of `A` or `B` i.e providing high residuals.

![ra_grade](../images/ra_feature_level.png)

This is an interesting observation. That means that the model is making errors if a `good looking` application defaults.

