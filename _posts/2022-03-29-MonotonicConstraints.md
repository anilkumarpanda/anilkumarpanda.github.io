---
layout: post
title: Monotonic Constraints for Boosting Models.
---

Boosting models like XGBoost, LightBoost have been some of the go to model for tabular datasets.This is because these models are highly performant and are able to learn various non-linear relationships within the datasets.However sometimes in the real world,creating an high performant model can result in a non-intuitive model. There are also requirements to include domain knowledge into the ML models.

Monotonicity constraints (MC), help us to achive the above objetives. Adding MC constraints helps with :

* Creating `interpretable` boosting models.
* Incorporating domain knowledge into the ML models.

This generally leads to models with less overfitting.
In this blog post, we will compare two models created on the same dataset without and with MC. We will compare the model performances and further improve on them if required.


To be continued...