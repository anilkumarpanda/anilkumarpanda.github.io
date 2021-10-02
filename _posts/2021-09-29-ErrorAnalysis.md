---
layout: post
title: Error Analysis for Tabular Data
---

Error analysis is an great method, for finding out where you ML model is making mistakes.There are some great videos/ blogs about how to do error analysis for text/image data. e.g video by Andrew Ng.

However I could not find anything related to error analysis for tablular data. One of the reason, I can think of is that it is intuitively diffcult to look at tabluar data and see if the model is misclassifying the data. 
Sure there many python packages that help you to do that. e.g erroranalysis , mealy etc .
However they are limited to showing you how to use the library and not how to use the error analysis methods to improve model performance. We will be using some of these in this blog post.

A model misclassifaction can be due to many reasons :

1. The data point has data quality issue. E.g loan given to a 300 year old person.
2. The data point is an outlier. E.g a very wealthy person defaulting on a small loan. 
3. There are very few examples for the model to learn. E.g There are only 5 customers with an car loan, thus the model has not learnt much from this dataset.
4. Model bias : Due to the inherit limitations of the model,the classification hasn't been done correctly. E.g Linear model assumptions.

With error analysis we can identify which subset of the dataset the model is making the most mistakes and then try to improve upon it. 
Thus we can look inot are the problematic features, and what are the typical values of these features for the mispredicted samples. 
This information can later be exploited to support the improvement strategy. Which can one of the following as mentioned on the [Dataiku website](https://doc.dataiku.com/dss/latest/machine-learning/supervised/model-error-analysis.html)

1. Improve model design: removing a problematic feature, removing samples likely to be mislabeled, ensemble with a model trained on a problematic subpopulation;

2. Enhance data collection: gather more data regarding the most erroneous or under-represented populations;

3. Select critical samples for manual inspection thanks to the Error Tree, and avoid primary predictions on them using model assertions. 

All of these are interesting options in this blog post I will focus on the 1 option.

