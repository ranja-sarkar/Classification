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

