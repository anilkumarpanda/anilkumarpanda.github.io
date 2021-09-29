---
layout: post
title: Error Analysis for Tabular Data
---

Error analysis is an great method, for finding out where you ML model is making mistakes.There are some great videos/ blogs about how to do error analysis for text/image data. e.g video by Andrew Ng.
However I could not find anything related to error analysis for tablular data. 
Sure there many python packages that help you to do that. However they are limited to showing you how to use the library and not how to use the error analysis methods to improve model performance. 

One of the reasons, I can of is , it is intuitively diffcult to look at tabluar data and see if the model is misclassifying the data. The misclassifaction can be due to many reasons :

1. The data point has data quality issue. E.g loan given to a 300 year old person.
2. The data point is an outlier. E.g a very wealthy person defaulting on a small loan. 
3. There are very few examples for the model to learn. E.g There are only 5 customers with an auto loan, thus the model has not learnt much from this dataset.
4. Model bias : Due to the inherit limitations of the model,the classification hasn't been done correctly. E.g Linear model assumptions.

I will try to explore this in this blog. Though I dont have a concrete plan of how to approach the various scenarios.

Plan :

1. Create a simple model on your favorite dataset. I will choose the german credit card dataset. 
2. Identify the data subsets that the model is making the most mistakes, both false postive and false negative cases.
3. Identify the most important features eg using SHAP values.
4. For the mislabelled datapoints, engineer new features.
5. Retrain the model and evaluate the model performance.