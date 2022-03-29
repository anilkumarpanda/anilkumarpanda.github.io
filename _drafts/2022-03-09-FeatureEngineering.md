---
layout: post
title: Feature Engineering
---

One of the things I like about the field of machine learning is that it is an constantly evolving discipline. There are always hundreds of different things to try, to explore and learn from.One of such things that caught my attention is the [Atom package](https://tvdboom.github.io/ATOM/v4.12/), especially the Deep Feature Synthesis and Genetic Feature Synthesis features.

* Deep Feature Synthesis applies standard mathematical operators (addition, subtraction, multiplication, etc…) on the existing features, making combinations of these. For example, DFS could create new features x1+x2,x3*x4 etc.

* GFG uses genetic programming, a branch of evolutionary programming, to determine which features are successful and create new ones based on those. Where DFS tries combinations of features blindly, GFG tries to improve its features with every generation of the algorithm. GFG uses the same operators as DFS, but instead of only applying the transformations once, it evolves them further, creating nested structures of combinations of features. Using only operators add (+) and mul (x), an example feature could be:
add(add(mul(x1, x2), x3), mul(x3, x4))

In this post, we will use this package on the [FICO dataset](https://community.fico.com/s/explainable-machine-learning-challenge) and see if we are able to improve the [model performance](https://anilkumarpanda.github.io/ErrorAnalysis/)
