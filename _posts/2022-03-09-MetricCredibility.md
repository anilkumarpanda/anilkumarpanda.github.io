---
layout: post
title: ML Model Metric Credibility
---

"How confident are you that the model performance (on test data) is not below 0.75 AUC ?".I came across this question in my work.This inspired me to write this blog.

Generally we calculate the model performance on an holdout test dataset. For example if you are working in the risk domain, you would train your model on historical data and the latest data for which performance can be measured will be used as test set.

We will get a certain model performance on the test data. How confident are we, that the model performance is above a certain threshold on a similar dataset? Assuming the data characteristics have not changed. One way to do that is to calculate the model performance on another test dataset. Why not! The challenge is labelled data is quite hard to obtain in almost all scenarios. *If data is oil, good labelled data is gold.* So we cannot get another test dataset.

Well then , let's sample the test data and calculate the model performance ? In that case, I assume the model performance will be similar and based on the sampling parameters the results can vary. The assumptions of independence are not satisfied.

Is there a python package for it ?

Generally model KPI's have a lower limit. Businesses would gladly accept a model with higher performance in the real world than reported at the time of development. The inverse would not be true. That is to say model performance below a lower limit will be unacceptable and the model would not be used.

For example, in classification setting roc-auc is a standard KPI. Lets say the minimum KPI for ROC-AUC is 0.75 for your project.If we have roc-auc on the test data of 0.8. What are the chances that given more data, the model performance on the test data would drop below 0.75 ?

[Model Validation Toolkit's](https://finraos.github.io/model-validation-toolkit/) can help us to calculate that. A detailed explanation can be found in  the [credibility section](https://finraos.github.io/model-validation-toolkit/docs/html/credibility_user_guide.html). TL;DR they use [beta-distribution](https://en.wikipedia.org/wiki/Beta_distribution) to do that.

Let's take the example for the [model](https://anilkumarpanda.github.io/ErrorAnalysis/) I created for the FICO challenge.
The model test performance is 0.79. After plugging in the required variables,

```python
from mvtk import credibility
# Number of positive samples in the test set
positives = 1539
# Number of negative samples in the test set
negatives = 1420
# ROC-AUC of the model
roc_auc = 0.79
# ROC-AUC cutoff
cutoff = 75/100
auc_positives, auc_negatives = credibility.roc_auc_preprocess(positives, negatives, roc_auc)
prob_below = credibility.prob_below(auc_positives, auc_negatives, cutoff) * 100
print(f'Probability of ROC-AUC being below {cutoff} is : {prob_below:.2f}%')

```

We see that the probability of ROC-AUC being below 0.75 is : 0.00% Sweet !!
So we can be confident that given more data(without drift), our model AUC will most likely not drop below the cut-off.

Similarly, we can also calculate the metric credibility for other performance measures like precision,recall etc.
