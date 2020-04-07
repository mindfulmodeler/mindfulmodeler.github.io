---
published: false

layout: post
title: "Machine learning notes"
date: 2019-07-02
description:
img:  # Add image post (optional)
fig-caption:
tags: [machine learning, modeling, simulation, algorithms, data science]
---
#MACHINE LEARNING
- all about applying algorithmic thinking and statistics in a way that facilitates effective computation. In order for ML to work, you must have a good grasp of basic statistical foundations, such as variance, bias, overfitting, and beyond.
- In data science, ML is all about building the right kind of mathematical model to gain insight into a large data set. The idea of "learning" happens when data scientists give the model adjustable parameters. The model is adjusted to fit existing (known) data, and then used to predict new (unseen) data.

**Principal Component Analysis**: a technique for extracting one or more dimensions that capture as much of the variation in the data as possible. PCA is a type of dimensionality reduction, which is useful when your data set has a large number of dimensions and you want to find a small subset that explains most of the variation. It involves repeatedly removing *principal components* until arriving at a low-dimension representation of the data. From this point, it is much easier to use standard techniques that work well on traditional (i.e. low-dimensional) data sets.



# Monte Carlo Simulations
A technique for generating random points as input for more operations  



## Machine Learning Pipeline
The first thing you do when implementing a pipeline is separate features and labels from the dataset
``X=winedf.drop(['quality'],axis=1)
Y=winedf['quality']``
