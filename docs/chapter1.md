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

Collecting complete information about a population is time-consuming and expensive, and sometimes not even possible. We need an appropriate sample size to infer about the population; in other words, we require a representative sample. 

Selecting a sample size to make a machine learn correctly, in other words to train an optimal model is a little tricky. There is typically a relationship between training datasize and model performance. However, for some model algorithms and datasets, such a relation might not exist at all. 

Power analysis helps estimate the minimum sample size required to detect an effect in a statistical test. A power curve yields the power of a test, which is power versus sample size for a given effect size. A hypothesis test which is a design-based approach figures out if an effect (small or not) is statistically significant to make us decide to change our minds on an action. The approach of calculating the sample size is based on effect size (es) of the test. 

<img width="374" height="299" alt="ss" src="https://github.com/user-attachments/assets/9289401d-2557-4588-ba55-a83e323abc61" />


We can estimate a sample size given the significance level denoted by alpha and power which is the probability of rejecting null hypothesis. It has been observed that larger sample sizes have the capability to detect small effects. 

We need enough evidence or sample size to perform a test, and the test statistic (metric) resulting out of it is called the probability value or p-value. If p-value is below a critical value (alpha), the null hypothesis is rejected and the default action is changed. This is the ‘frequentist’ approach which essentially tells us that there’s a default action and with each evidence or datapoint we either do not change our mind (null) or we do (alternative hypothesis). 

# Sensitivity

Sensitivity analysis forms the basis of testing different (model) algorithms and their configurations, with the sample (train data) size. By algorithm configuration, I mean statistical heuristics such as number of labels in the (labelled) dataset, number of input features, number of hyperparameters, etc. This helps in evaluating an algorithm for a task and estimating the sample size needed to build an optimally performing predictive model. 

It is noteworthy at this point that I mentioned earlier hypothesis testing is a design-based approach, while machine learning is a model-based approach, both are statistical approaches with different treatments.

Coming back to sensitivity, it provides an approach to quantify the relationship between model performance and data (consumed by the model) for a given problem. Datasets may be too small to effectively capture the capability of a predictive model or too large where data augmentation might not improve model performance. A learning curve yields the sensitivity of the model, which is model performance versus data size. It tells how sensitive the model is to the size of data used for training.

There might exist an upper bound on the datasize for a given dataset and model algorithm, beyond which there's no change (saturation) in estimated performance of the model.  

Please note that expanding data vertically means increasing the number of training examples (rows), which is datasize. Expanding data horizontally means increasing the number of features/variables (columns) in tabular data, which is data volume. 

We cannot assume adding more datapoints would lead to better performance of the model. There are two forces at play here viz., how well the model fits the data, and how reliably the fit generalizes and extends to unseen data. 

-----

Having discussed effect and effect sizes, it is mentionworthy that the practical significance of effect sizes can only be judged with respect to the context or problem at  hand. In some cases, “small” effects are practically significant and in some other, “large” effects are not that is, they are not significantly meaningful wrt the context. 

# Statistical significance *vs* Practical significance

In the world of data, a common pitfall is the confusion between statistical significance and practical significance. Statistical significance is the likelihood that a test result is not random (due to chance), determined by a threshold or p-value. Practical significance, on the other hand considers whether the difference or effect size is large enough to be meaningful and relevant in a real-world context. 

In a hypothesis test, making the wrong decision (false alarm) is the significance level or alpha. The significance level represents the level of evidence for rejecting the null hypothesis. It is a Type I error. The probability of making a Type II error is beta. 

The p-value indicates the strength of evidence against the null hypothesis, smaller p-value indicates stronger evidence. To accept alternative hypothesis, the p-value must be lower than alpha, meaning there is an effect 95 out of 100 times if alpha = 0.05. To accept the null, the p-value must be larger than alpha; if alpha is 5% and confidence level is 0.95 (95%), it means there is no effect 95 times out of 100. 

Confidence interval of a test is a window/range of values constructed using significance level and confidence level. Size of the confidence interval for a given confidence level is determined by few factors.

a.	*sample size*
   
Larger the sample size, more certain you’re of the results reflecting the population; smaller is the confidence interval however, the relationship between sampe size and confidence interval is not linear.

b.	*percentage of sample*
   
The accuracy of results truly reflecting the population depends on the percentage of sample that picks a particular result. This is related to the margin of error. For a given accuracy, one has to determine the percentage of sample and vice versa.

c.	*population size*
   
This is most of the times unavailable, hence an appropriate sample size becomes essential.

Let us consider an example to understand statistical significance and practical significance better. Assume a company selling a product is testing the effectiveness of two different marketing campaigns or strategies for the product. Group 1 of customers receives Marketing Strategy A, and Group 2 receives Marketing Strategy B. After 4 weeks, the average purchase amounts in both groups are recorded.

➡ Group 1 (Marketing Strategy A): Mean purchase amount : $100.00

➡ Group 2 (Marketing Strategy B): Mean purchase amount : $100.25

We also find that the p-value (test statistic) turns out to be extremely low, suggesting that the observed difference in purchase amounts is statistically significant and unlikely due to random chance.

However, an average increase of $0.25 in customer spending may not be meaningful in practical terms to justify a change in marketing strategy, although the difference in purchase amounts ($0.25) is statistically significant resulting out of the test. It therefore becomes essential to assess both statistical and practical significances to make informed and effective business decisions. 

# Evaluating classifiers

Let us consider an example of diagnosis of a pregnant woman, whether she is pregnant or not. Actual values can be true (she's pregnant) and false (she's not pregnant). 

Predicted values can also be 1 (she's pregnant) and 0 (she's not pregnant). So the confusion matrix of outcome yields the four categories of results shown below.

<img width="407" height="251" alt="class" src="https://github.com/user-attachments/assets/5556f5d2-4e89-4e04-b234-148f8c6e5f86" />

A false alarm is Type I error, and a miss (false negative) is Type II error. A false alarm (FP) is positive prediction when it is actually false. A miss (FN) is negative prediction when it is actually true, that is you miss the right signal. 

