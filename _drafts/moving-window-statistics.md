---
published: false

layout: post
title: Moving Window Statistics in Python
date: 2020-01-26
description: How to perform a rolling or moving average over an array. 
img:  
fig-caption:
tags: []
categories: [Tutorial]
---

1. TOC
{:toc}
{:.toc-styling}

# Moving Window Statistics
- Calculation performed by subsetting the data into "windows" and performing the calculation on the subsets of the full data
- Commonly, this technique is used to cut through the "noise" in a dataset. You can think of this as a way of "smoothing out" the bumps in your data.
- You can find many examples of moving windows using time series data, where the window looks "back" and "forward" per data point. I found this to be relatively easy with timeseries data, with many examples (especially in economics and signal processing) and in-built functions for how to calculate this. But there are few tutorials covering options for making a square window (e.g. 3x3) that can perform a variety of statistical computations which is useful for smoothing out spatial variability of a dataset, for instance
In the following tutorial, I'll cover three different ways built-into Python, as well as a custom function that is easy to follow and adapt to your own uses

**Important Tip: Use Test Arrays**
If you're turning to a language like Python to automate a complex, moving statistic - I'm betting that your dataset is rather large and complicated. Make sure you use a very simple test array to make sure that the calculations are working like you expect them to!

## Method 1: Rolling Windows in Pandas

## Method 2: Scikit learn image processing

## Method 3: Numpy

## Method 4: Custom Function (Weighted Moving Average)

### Conclusion
Many datasets contain noisy spikes that detract from the true behavior underlying the system. Performing a rolling window function can be very useful and doesn't have to be hard. Make sure to have a sample dataset on hand to ensure that your calculations are running correctly. Be sure to try out different window sizes and shapes until you find one that suits your needs!
