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

We discuss the well-known metrics for evaluating a classifier. Not all of them are useful in every case. We must choose the ones in accordance with the business context and problem at hand.

## Precision, Recall, F1-score

*Precision* of the classifier is important when we believe False Positives (FPs) are more important than False Negatives (FNs) for example, in spam email detection.

*Recall* is important when we believe FNs are more important than FPs for example, in cancer detection. There often exists a trade-off; designing a model with high recall will identify most people that have cancer (TPs), saving their lives but at the cost of mis-diagnosing healthy individuals as having cancer (FPs), subjecting them to expensive and dangerous treatments like chemotherapy.

On the other hand, designing a model for precision yields confident diagnoses (someone predicted as having cancer very likely does have cancer), but at the cost of failing to identify everyone who has the disease (FNs), resulting in potentially fatal consequences for those left undiagnosed. In this example, FNs result in death, the classification threshold should likely be set to optimize recall over precision.

Precision and recall are useful in cases where classes are not evenly distributed that is, data is not balanced. The common example is the prediction of whether or not someone has a disease, if only a small percentage of the population (let's say 1%) has this disease, we could build a classifier that always predicts that the person does not have the disease, we would have built a model which is 99% accurate and 0% useful. 

It is important to understand and decide ahead of time what's more consequential - FPs or FNs to investigate how the trade-off manifests in a particular dataset, and design the classifier model accordingly.

In situations where either precision or recall are poor, the **F1-score** is poor too. F1-score is a harmonic mean of the two measures which varies between 0 and 1. Only when both precision and recall have good performance, the F1-score is high. However, the F1-score is a good way to compare the performance of multiple classifiers and rank them accordingly. 

Accuracy is its highest at the maximum of F1-score, but it barely changes thereafter.

When choosing between multiple models, all with varying values of precision and/or recall, F1 may be used to determine which one produces optimal results for the problem at hand.

The F1-score is not suitable for every classification problem, for example it's misleading for imbalanced classes. So if TNs are important, considering a different metric such as specificity is worthwhile. 


### Sensitivity, Specificity

Sensitivity (true positive rate) is the proportion of observed or actual positives (Yes) that were predicted to be positives (Yes).
Specificity (true negative rate) is the proportion of observed or actual negatives (No) that were predicted to be negatives (No).


Every test/model needs to pick a threshold which can be 0.5. As an example, in transactions data we need to specify how high the probability of fraud has to be before we call the transaction a fraudulent one, and is particularly crucial as the number of fraudulent transactions typically happen to be much lesser than legit ones. 

So sensitivity tells us out of all actual fraudulent transactions, what percentage were predicted by the model to be so. Specificity tells us out of all actual legit transactions how many were predicted to be legitimate. Lowering the threshold to increase sensitivity will decrease specificity and viceversa. Increasing sensitivity in turn is decreasing wrong identification (false negative) of a legit user as fraud. 

It is important to choose the right threshold for a given dataset, to know how much tradeoff is possible between being sensitive and specific. 

## ROC

The ROC (receiver operating characteristic) curve provides a visual way to observe changes in the model’s performance with the classification or decision thresholds. The curve helps select thresholds that allow our model to identify as many TPs while minimizing FPs. 

Let’s say our model classifies airplanes from clouds in radar signals. We will assess performance of the classifier model with the number of TPs and FPs it predicts.

TPR is the probability that a positive sample is correctly predicted in the positive class, and FPR is the probability that a negative sample is incorrectly predicted in the positive class. We will construct a graph with True Positive Rate (in the y-axis) and False Positive Rate (in the x-axis). We change (x, y) values by dragging a threshold between values 0 and 1. 

We start at the classification threshold equals 0, where everything will be classified as an airplane yielding TPR & FPR both equal to 1. This model correctly classifies every airplane as an airplane, it also incorrectly classifies every cloud noise as an airplane.

We increase the threshold to new ones where the model classifies some clouds as airplanes. We try all possible values of the threshold and see how TPR & FPR change, while keeping in mind that our goal is to find the threshold that best maximizes TPR and minimizes FPR.

There's no perfect (TPR = 1) classifier, regardless of FPR. If the result shows a perfect classifier (points to overfitting or data-leakage), we have to make sure that there’s no place where the training data is leaking information about the class/label, which wouldn’t be available when the model’s deployed. A random (TPR = FPR) classifier only means the data has no predictive power. Well, anything below it (TPR < FPR) is not worth considering.

We continue to increase the threshold until it reaches 1. As we drag the threshold, we understand the classifier as a function of the threshold. The graph we get is the ROC curve which helps understand potential strengths and weaknesses of the classifier. Which classification threshold to choose between 0 and 1 for our model totally depends on how much trade-off in TPR & FPR the business or problem at hand allows us to make. 

Depending on the consequences of the action, we will use a threshold to make the decision. In some cases, one might even have three different decisions, although there’re only two classes (sick versus healthy for example) - "go home & don't worry" versus "run another test” (the one we’ve is inconclusive) versus "operate immediately".

Any measure of optimality for classification which ignores costs does so at its own risk. Even the ROC AUC (area under curve) fails to be cost-invariant - AUC ranges in value from 0 to 1, with higher numbers indicating better performance. A perfect classifier will have an AUC of 1, while a perfectly random classifier an AUC of 0.5. A model that predicts that a negative sample is more likely to have a positive label than a positive sample will have AUC of 0, indicating severe failure at the modeling end. Scores in the range [0.5, 1] imply good performance, while anything under 0.5 indicates very poor performance.

AUC is the probability that the model will rank a randomly chosen positive example more highly than a randomly chosen negative example. In cases when we desire well-calibrated probability outputs that is, when we care about the true likelihood of an event and not just model performance, ROC AUC yields no useful information. Additionally, the AUC metric treats all classification errors equally, ignoring the potential consequences of ignoring one type over another.

## Accuracy

Accuracy, the proportion of correct classifications among all or total number of classifications is a simple intuitive measure, yet it may be a poor measure for imbalanced data. 

Accuracy assigns equal cost to FPs and FNs. When the dataset is imbalanced - say it has 99% of instances in one class and only 1 % in the other, there is a great way to lower the cost, which is predicting that every instance belongs to the majority class,get accuracy of 99% and go home early. The problem starts when the actual costs that we assign to every error are not equal.

If we deal with a rare but fatal disease, the cost of failing to diagnose the disease of a sick person is much higher than the cost of sending a healthy person to more tests. Accuracy certainly is not useful in such cases.



# Summary

Generally speaking, there is no “best” measure for assessing classifiers. The best measure is derived from our needs, in short it is driven by a business question and not a modeling question. It is common that two people may use same dataset but choose different metrics due to different goals.

There is a cost (or benefit) structure to consider when using a machine to learn and suggest, or to make decisions on behalf of people. All information is embedded in a cost matrix with entries corresponding to those of the confusion matrix of a classifier model. Since this information is a function of the people who are considering mechanistics to help decision-making, it is subject to change with the circumstances, and therefore there is never going to be one fixed measure of optimality which will work all time.

When it comes to evaluating a classifier or any model for that matter, such metrics are by no means exhaustive. Many other techniques of assessment of classifiers exist including probability calibration, diagnostic tools (likelihood ratios, etc.). While the concepts are explained in the context of binary classification, they can be applied to multiclass classification tasks as well.

