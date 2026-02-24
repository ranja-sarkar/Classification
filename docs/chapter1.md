---

title: Binary classification

description: Binary classification

layout: default

nav_order: 2

parent: Overview

---


Statistical tests use a data sample to assess and make an inference about a population from which the sample is drawn. In a two-sample comparison, the goal often is to assess whether the means of some attribute obtained for individuals in the two samples (sub-populations) differ. Statistical power (simply power) is the probability of detection of an effect, quantified by a size called effect size, in other words the probability that the test will find a statistically significant difference between that attribute in the samples. When there exists an actual effect, the power of a test represents the chances of effect detection.

# Power

Power depends on a number of factors for effect detection, few of which pertain to a specific testing situation. The ones power almost always depends on are significance level used in the test, magnitude of the effect-of-interest (effect of size), and size of the sample. Power versus sample size yields the power curve which tells us how adequate the size is to detect a significant effect in a test (experiment) or randomized controlled trial (RCT).

The power of a test is the probability that the test correctly rejects the null hypothesis when the null is false. So it is the true positive rate (TPR). Power value ranges from 0 to 1. As the power increases, false alarms (false positives) reduce wherein FP is the probability to (incorrectly) reject the null when it is true.

<img width="319" height="278" alt="power" src="https://github.com/user-attachments/assets/5c135105-2ada-4861-b9ac-df5c2640f0f1" />

Collecting complete information about a population is time-consuming and expensive, and sometimes not even possible. We need an appropriate sample size to infer about the population; in other words, we require a representative sample. Selecting a sample size to make a machine learn correctly, in other words to train an optimal model is a little tricky. There is typically a relationship between training data-size and model performance. However, for some model algorithms and datasets, such a relation might not exist at all. 

Power analysis helps estimate the minimum sample size required to detect an effect in a statistical test. A hypothesis test which is a design-based approach figures out if an effect (small or not) is statistically significant to make us decide to change our minds on an action. The approach of calculating the sample size is based on effect size (es) of the test. 

<img width="374" height="299" alt="ss" src="https://github.com/user-attachments/assets/9289401d-2557-4588-ba55-a83e323abc61" />


We can estimate a sample size given the significance level (alpha) and power which is the probability of rejecting null hypothesis or of detection of an effect.
It has been observed that larger sample sizes have the capability to detect small effects. 
We need enough evidence or sample size to perform a test, and the test statistic or metric resulting out of it is the p-value. If p-value is below a critical value (significance level), the null hypothesis is rejected and the default action is changed. This is the ‘frequentist’ approach which essentially tells us that there’s a default action and with each evidence or datapoint we either do not change our mind (null) or we do (alternative hypothesis). 


