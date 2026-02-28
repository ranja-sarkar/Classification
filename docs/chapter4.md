---

title: Calibrating classifier

decsription: Calibrating classifier

layout: default

nav_order: 5

parent: Overview

---

A classifier’s outcome with calibrated probability must match the true probability.

For example, if a calibrated classifier model assigns a probability of 0.6 to class 1 in 100 samples, 60 of those samples must truly belong to class 1. In effect, the predictions or probability estimates returned by the classifier should reflect the true occurrences (likelihood) and if they do not, they ought to be corrected by calibration.

