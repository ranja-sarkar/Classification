---

title: Binary classification

description: Binary classification

layout: default

nav_order: 2

parent: Overview

---


Statistical tests use a data sample to assess and make an inference about a population from which the sample is drawn. In a two-sample comparison, the goal often is to assess whether the means of some attribute obtained for individuals in the two samples (sub-populations) differ. Statistical power (simply power) is the probability of detection of an effect, quantified by a size called effect size, in other words the probability that the test will find a statistically significant difference between that attribute in the samples. When there exists an actual effect, the power of a test represents the chances of effect detection.

Selecting a sample size to make a machine learn correctly, in other words to train an optimal model is a little tricky. There is a typical relationship between training datasize and model performance. However, for some model algorithms and datasets, such a relation might not exist at all. 

# Power

Power depends on a number of factors for effect detection, few of which pertain to a specific testing situation. The ones power almost always depends on are significance level used in the test, magnitude of the effect-of-interest (effect of size), and size of the sample. Power versus sample size yields the power curve which tells us how adequate the size is to detect a significant effect in a test (experiment) or randomized controlled trial (RCT).

The power of a test is the probability that the test correctly rejects the null hypothesis when the null is false. So it is the true positive rate (TPR). Power value ranges from 0 to 1. As the power increases, false alarms (false positives) reduce wherein FP is the probability to (incorrectly) reject the null when it is true.

<img width="319" height="278" alt="power" src="https://github.com/user-attachments/assets/5c135105-2ada-4861-b9ac-df5c2640f0f1" />

Collecting complete information about a population is time-consuming and expensive, and sometimes not even possible. We need an appropriate sample size to infer about the population; in other words, we require a representative sample. 

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

## Evaluation Metrics

We discuss the metrics defined to assess or evaluate classification models. 

### Precision and Recall

Precision is the number of TPs out of all positive predictions. Precision counts how many classifications are relevant. A measure of classifier quality is the precision. In a fraud prediction model precision is more important, as incorrectly accusing a legit transaction while trying to catch a fraudulent transaction has damaging consequence on the customer. Precision ensures we’re not misclassifying too many legit transactions. 

<img width="116" height="17" alt="pp" src="https://github.com/user-attachments/assets/3a374998-58ef-415c-ace2-9b4a3496124c" />

Wrong rejection is a miss for example, a legit user is incorrectly rejected by a system as a fraud. Wrong acceptance is false alarm that is, a fraud is incorrectly accepted by the system as legit. 

Recall is the number of TPs out of all positive actuals. It is called sensitivity too. Recall counts how many classifications are true. It is thus a measure of quantity. 

<img width="112" height="25" alt="rr" src="https://github.com/user-attachments/assets/691ba0db-06c1-4cff-b851-f1a343190805" />

In a churn prediction model recall is more important, for awareness of potential churners. Recall ensures we’re not overlooking actual churners. 

### F1-score

This score is a harmonic mean of recall and precision and manages the trade-off between quantity and quality of classifications.  Using a harmonic mean ensures that if either precision or recall is low, then the F1 score drops significantly for the classifier.

<img width="366" height="41" alt="f1" src="https://github.com/user-attachments/assets/73296b8c-6cf8-42c7-80fe-438aa70671e0" />

It is most worthwhile to choose a metric based on the business problem we are solving because there are always trade-offs. The metric selection must be based on how much trade-off the business allows. Detection (or not) of a true effect is related in a natural way to the cost analysis of diagnostic decision-making.

---

A little know-how in here would be comprehending that upon introduction of an exponent in the mathematical expression of 'mean' making it a 'generalized mean', one can arrive at an entire spectrum of 'means'. 

<img width="254" height="58" alt="mm" src="https://github.com/user-attachments/assets/14c029f8-0e89-40c2-bce0-81da6a6d6a07" />

For example, the exponent p=1 yields arithmetic mean and p = 2 yields root mean square or quadratic mean. We must know that numbers add up for an arithmetic mean, reciprocals of numbers add up for a harmonic mean, squares of numbers add up for a quadratic mean, and so on. 

---

Now let us return to our main topic 'metrics'.

### ROC curve

The ROC (receiver operating characteristics) curve is a plot of power (TPR) as a function of false positive rate (FPR), when model performance at varying threshold values is calculated from the sample. 

Each classification result from the confusion matrix represents one point in the ROC space. ROC is the recall. Specificity of the classifier model is defined as TNR that is, TN/(TN+FP). So ROC is sensitivity versus (1-specificity). 

<img width="490" height="388" alt="roc" src="https://github.com/user-attachments/assets/a488b0b2-80ab-4cb4-8882-1e89f5ec8a7d" />

Higher the TPR (power), higher is the chance of detecting a false alarm. However, the ROC curve does not yield the model precision. The diagonal divides the ROC space. Points above the diagonal represent good classification results (better than random); points below the line represent bad results (worse than random).

<img width="425" height="363" alt="rr-aa" src="https://github.com/user-attachments/assets/017c8810-cb9c-4f4a-ab28-d72f2f9b2e90" />


Area under the curve is AUC, the ROC-AUC summarizes sensitivity and specificity, but does not inform regarding precision. Also, two ROC curves with equal AUC may yield different outcomes. 

![auc](https://github.com/user-attachments/assets/71867635-e53e-4bb7-b30c-92c0911eaf17)

A random classifier has AUC = 0.5 in the ROC curve. A presion-recall curve in addition to ROC curve is useful for explainability.

<img width="263" height="220" alt="pr" src="https://github.com/user-attachments/assets/6e7f04b4-c074-41ab-ab3a-d5a66d706749" />

While the ROC curve is recall *vs.* fallout, a precision-recall curve as the name suggests is a precision vs. recall or sensitivity. The ROC analysis helps in interpretations and selection of optimal models and discard suboptimal ones independently from the class distribution.  


### Accuracy

The accuracy metric is the percentage of correct predictions that is, number of correct predictions out of all predictions.

<img width="181" height="29" alt="aa" src="https://github.com/user-attachments/assets/19e2a43f-6654-4b4e-ab80-516751e0a65e" />

Accuracy alone is not too informative about the effectiveness of a classifier model. A perfect classifier for which AUC = 1.0 does not exist in reality.

<img width="443" height="196" alt="auc1" src="https://github.com/user-attachments/assets/81aa8402-c3b8-4907-956f-9b204d46ddc0" />
<img width="445" height="167" alt="auc2" src="https://github.com/user-attachments/assets/5fe1adb0-6df8-4fee-b727-2bfeb5f51f2f" />


It can be misleading for imbalanced data, wherein the probability or classification threshold shifts. This threshold value is 0.5 for balanced data. The accuracy metric can be a good enough measure for imbalanced data (like in fraud detection or churn prediction cases) if the classification threshold is tuned properly while training the model. 

# Summary

We understand by now that recall is completeness and precision is exactness of the classification model, and that how essential it is to correctly choose the metrics for evaluation of the classifier model.  

There are costs associated with Type I (detecting a false effect)  and Type II (failing to detect a true effect) errors and in most business contexts, the latter is considered to be more severe as it may lead to damaging consequences, and the former  can be mitigated in short-term. Different types of mis-classifications incur different costs. When different misclassification costs are assigned to different classes, it can skew probability estimates of a classifier model, which may adjust its decision boundary to minimize overall cost. This can potentially lead to uncalibrated predictions of categories. Hence, prediction confidence is as important as the (point) prediction itself. Cost-sensitive learning is when the model (e.g. logistic regression) is trained with a cost function that assigns a higher cost to misclassifying the minority class. 
 
