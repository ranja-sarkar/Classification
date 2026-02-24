---

title: Assessing classifier

description: Assessing classifier

layout: default

nav_order: 4

parent: Overview

---

Assessing classifier models requires careful considerations. What the classifier outputs is a probability and the classification threshold is a value we use to translate this probability into (discrete) output or binary categories in case of a binary classification and multi-categories in case of multiclass classification. The probability is compared with the threshold value which is used to bin values into distinct categories. 

Let’s say we've trained a binary classifier to diagnose an individual as having cancer or not; if our classification threshold is 0.5, we'll classify any patient with a probability greater than 50% as cancer-positive, and a patient with a probability less than 50% as cancer-free.


# Metrics


## Precision, Recall, F1-score

## Sensitivity, Specificity

## ROC

## Accuracy

Accuracy, the proportion of correct classifications among all or total number of classifications is a simple intuitive measure, yet it may be a poor measure for imbalanced data. 

Accuracy assigns equal cost to FPs and FNs. When the dataset is imbalanced - say it has 99% of instances in one class and only 1 % in the other, there is a great way to lower the cost, which is predicting that every instance belongs to the majority class,get accuracy of 99% and go home early. The problem starts when the actual costs that we assign to every error are not equal.

If we deal with a rare but fatal disease, the cost of failing to diagnose the disease of a sick person is much higher than the cost of sending a healthy person to more tests. Accuracy certainly is not useful in such cases.



# Summary

Generally speaking, there is no “best” measure for assessing classifiers. The best measure is derived from our needs, in short it is driven by a business question and not a modeling question. It is common that two people may use same dataset but choose different metrics due to different goals.

There is a cost (or benefit) structure to consider when using a machine to learn and suggest, or to make decisions on behalf of people. All information is embedded in a cost matrix with entries corresponding to those of the confusion matrix of a classifier model. Since this information is a function of the people who are considering mechanistics to help decision-making, it is subject to change with the circumstances, and therefore there is never going to be one fixed measure of optimality which will work all time.

When it comes to evaluating a classifier or any model for that matter, such metrics are by no means exhaustive. Many other techniques of assessment of classifiers exist including probability calibration, diagnostic tools (likelihood ratios, etc.). While the concepts are explained in the context of binary classification, they can be applied to multiclass classification tasks as well.

