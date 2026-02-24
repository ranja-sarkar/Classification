---

title: Assessing classifier

description: Assessing classifier

layout: default

nav_order: 4

parent: Overview

---

Assessing classifier models requires careful considerations. What the classifier outputs is a probability and the classification threshold is a value we use to translate this probability into (discrete) output or binary categories in case of a binary classification and multi-categories in case of multiclass classification. The probability is compared with the threshold value which is used to bin values into distinct categories. 

Let’s say we've trained a binary classifier to diagnose an individual as having cancer or not; if our classification threshold is 0.5, we'll classify any patient with a probability greater than 50% as cancer-positive, and a patient with a probability less than 50% as cancer-free.
