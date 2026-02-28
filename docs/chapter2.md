---

title: Multiclass classification

description: Multiclass classification

layout: default

nav_order: 3

parent: Overview

---

The confusion matrix of a binary-class classifier is simple, the predicted classifications are boxed into true positive (TP), false positive (FP), false negative (FN), and true negative (TN). The multi-class confusion matrix is converted into a one-vs-all matrix for each class, so that class-wise metrics like precision, recall, F1-score can be calculated. In the one-vs-all scheme, a classifier compares each class to all the other classes at once. 

![BCM](https://github.com/user-attachments/assets/c69eff54-a544-4abd-aa95-756bc11e4031)
![3CM](https://github.com/user-attachments/assets/a601662e-e7c1-44b3-9333-3229203d2081)
