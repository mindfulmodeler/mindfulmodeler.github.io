
# Standard Probability Models
How should uncertainty be handled when a system has some kind of randomness? There may be a range of outcomes that fall under some probability distribution. What you'd like to do is reduce the uncertainty band around some output to its "typical" value.

NOTE: Using a standard probability model may not work for all types of uncertainty, especially [deep uncertainty].

## 1. Bernoulli Trials and The Binomial Distribution
When a random trial can only end in one of two outcomes (success or failure), it is a **Bernoulli Trial**.
- Probability of success = p
- Probability of failure = 1 - p


# P-Values
Look at the tail of the normal distribution. The p-value is the probability that if you randomly pick a value from the population, that it will be greater than that level.
- when a p-value is less than alpha, it means that the outcome is statistically significant
- the alpha is just some threshold p-value (set at 0.05 for unknown reasons). If the area under the curve of a certain p-value is less than the alpha value, this is considered to be so rare an event that we call it 'statistically significant'.
- when the p-value is greater than the alpha, we 'fail to reject the null hypothesis'. In other words, the boring finding is more likely.
[ASA warning on Pvalues](https://www.nature.com/news/statisticians-issue-warning-over-misuse-of-p-values-1.19503?WT.mc_id=TWT_NatureNews&error=cookies_not_supported&code=2edb6732-0d05-48bb-a104-8c5e1e9ebf88)

# Z-Test (Similarity Test)
Is a sample similar to a population or not? Using classical statstics, the approach would be as follows:
1. generate a null and alternate hypothesis
2. calculate the z-score
3. determine the p-value
4. compare p and alpha
5. interpret the outcomes
