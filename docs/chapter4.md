---

title: Calibrating classifier

decsription: Calibrating classifier

layout: default

nav_order: 5

parent: Overview

---

A classifier’s outcome with calibrated probability must match the true probability.

For example, if a calibrated classifier model assigns a probability of 0.6 to class 1 in 100 samples, 60 of those samples must truly belong to class 1. In effect, the predictions or probability estimates returned by the classifier should reflect the true occurrences (likelihood) and if they do not, they ought to be corrected by calibration.

![c0](https://github.com/user-attachments/assets/74e5f01a-90b0-4400-9891-66281bb7fefa)

Many machine learning algorithms used for classification task like random forest, SVM often produce uncalibrated probability estimates. 
If we have two observations and the trained model scores them as 0.6 and 0.9, is there a higher chance that 0.9 score belongs to the positive class?
For some models, this is true but for others it might not be which means that the scores might not represent the true probabilities of outcomes.

Metrics such as accuracy focus solely on correctness, rather than certainty. Decision trees for instance, utilize Gini index to make splits, prioritizing classification accuracy over calibration. Similarly, SVMs prioritize widening the margin rather than optimizing probabilistic estimates. Deep neural networks often employ techniques like dropout to prevent overfitting, which may impact their calibration. Techniques of resampling used to address class imbalance can distort probability estimates that is, over-sampling may inflate minority class probabilities and under-sampling might underestimate majority class probabilities. 

Maximum margin algorithms such as adaptive boosting (e.g. AdaBoost), SVMs, and Naive Bayes yield uncalibrated probabilities. AdaBoost has a different optimization objective that does not produce calibrated probabilities which however does not imply an inaccurate model at all times, since classifiers are evaluated by their accuracy when creating a binary response. 

Logistic regression is designed to produce calibrated probabilities but the training sample size is important (see below). If we do not have a large enough training dataset, the model might not have enough information to calibrate the probabilities. Having said that, more data that is beyond a limit does not significantly improve the calibration. We must note that this depends on the dynamics of the data, we might need more or fewer data only depending on the use case.

![c1_LR](https://github.com/user-attachments/assets/80406f3c-928f-438b-82e8-ad8ae32311f5)

It is also essential to acknowledge that there are scenarios where calibration may not be necessary. While the main objective of model calibration is to ensure that the output probabilities are meaningful and interpretable, there are situations where calibration might not be crucial for instance, a scenario where a model is tasked with ranking the quality of news article titles and the goal is simple - identify the title with the highest score following a policy of selecting the top-ranked title. In such cases, calibrating the model may not offer significant benefits, as the focus is solely on identifying the best-performing title rather than interpreting probabilities.

Calibration of classifiers work by using the model’s (uncalibrated) predictions as input for training a second model that maps the (uncalibrated) scores to observed frequencies. We must use a new set of training data to fit the second model, else we will end up introducing bias in the model.  

The methods of calibrating a classifier are discussed wrt a binary classifier, however they can be extended to support multiple classes.

# Calibration methods

There are two widely used methods of calibrating a classifier, when the relationship between the model predicted probabilities and true probabilities is monotonic in nature.

## Platt Scaling

It is recommended when the data size is small, although calibration might lead to overfitting on smaller datasets therby making it non-beneficial. Extra care needs to be taken there. 

It works by applying a logistic regression on the classifier score. 


The classifier output is f(x) where x is the score, where A and B are two parameters that are learned by the algorithm.

## Isotonic Regression

It is a non-parametric form of regression and better used when we have large datasets. It learns a piecewise linear function to map the classifier score to calibrated probability, and can correct monotonic distortion in predictions.

# Calibration metrics

Commonly used metrics to evaluate the effectiveness and quality of calibration are Brier score and log loss. 

A calibration curve or reliability curve is a graphical representation of the calibration. It allows us to benchmark our model against a target and compare several models. For example, if we want to deploy a well-calibrated model into production, we might train several models and then deploy the one that is better calibrated. Models whose predictions can be better calibrated are random forests, SVMs, and neural networks. Having said that, it is also important to remember that calibration adds complexity to the development and deployment process. So before attempting to calibrate a model, we must ensure there are not any more straightforward approaches such as better quality data or algorithms whose results are in general well-calibrated (e.g. logistic regression). 

![cc](https://github.com/user-attachments/assets/edcf026d-b25d-41c8-8b7a-8e07af7eef2a)

The calibration curve plots the mean predicted probability against the true fraction of positive samples. A perfectly calibrated model follows a diagonal line, where the x-axis represents the model’s predicted probability and the y-axis shows the (actual) fraction of positive samples for each probability bin, where binning can be equal-width or equal-frequency.

