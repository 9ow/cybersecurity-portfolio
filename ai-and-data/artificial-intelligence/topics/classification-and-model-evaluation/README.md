# Classification and Model Evaluation

> **Provenance:** Uploaded *Introduction to Machine Learning with Scikit-learn* PPT explicitly introduces classification vs regression, train/test separation and mentions evaluation metrics; previous repository text contained KNN, logistic regression, cross-validation, and extended metric descriptions. Those additional concepts below are **supplemental background retained from the existing repository**, not asserted to be covered in the four uploaded lecture decks or personally implemented.

## Predicting classes versus numeric quantities

**Classification** predicts one of several discrete labels (for example spam/legitimate or a fruit category). **Regression** predicts a continuous quantity (for example electricity charges under a supplied linear rule). In multiclass classification, integer-encoded classes still represent **categories**, not a meaningful numeric continuum. A training sample is `(X_i, y_i)`; a fitted estimator predicts labels `ŷ_i` for held-out observations. Training success is not the same as reliable testing or operational detection.

The slides introduce `train_test_split(test_size=..., train_size=..., random_state=..., shuffle=...)` and list 70/30, 80/20 and 90/10 as examples. A held-out test set is for evaluation; avoid tuning decisions on it repeatedly. Class imbalance means plain accuracy can mislead.

## Confusion matrix and classification metrics — supplemental explanation

For **binary** predictions, TP = correctly predicted positive; TN = correctly predicted negative; FP = negative predicted positive; FN = positive predicted negative.

| Metric | Formula | What it answers | Limitation |
| --- | --- | --- | --- |
| Accuracy | `(TP+TN)/(TP+TN+FP+FN)` | Overall fraction correct | Can hide failure on rare classes |
| Precision | `TP/(TP+FP)` | Of predictions called positive, how many were correct? | Does not capture missed positives |
| Recall / sensitivity | `TP/(TP+FN)` | Of real positives, how many did we find? | Does not measure false-alarm volume |
| F1 | `2·precision·recall/(precision+recall)` | Harmonic balance of precision and recall | Ignores TN directly |

Metrics can be undefined when a denominator is zero; report the metric policy rather than hiding zero-division behavior. In **multiclass** evaluation, use per-class scores and specify **macro** (unweighted mean of class metrics), **weighted** (support-weighted) or **micro** (aggregate TP/FP/FN), with the label order of the confusion matrix. For imbalanced datasets with rare classes, per-class recall and macro-F1 deserve attention.

```python
# Illustration only: the model must be fitted elsewhere before this code works.
from sklearn.metrics import classification_report, confusion_matrix
# y_pred = fitted_classifier.predict(X_test_scaled)
# print(confusion_matrix(y_test, y_pred))
# print(classification_report(y_test, y_pred, zero_division=0))
```

The code is intentionally commented out because **no verified fitted classifier and test predictions were supplied**.

## Algorithms mentioned in earlier repository material — supplemental

**K-nearest neighbors (KNN):** a new point is compared with training points under a distance measure, the `k` nearest are found, and a majority vote predicts the class. Euclidean distance for features `x,z` is `d(x,z)=sqrt(sum_j (x_j-z_j)^2)`. Small `k` may overreact to noise; large `k` may wash out minority structure; the feature scale changes distances. Earlier repository text discussed a two-apple/one-orange illustrative vote, but no source deck or independent calculation was included for that exercise.

**Logistic regression:** compute linear score `z=w·x+b` and transform to a binary-class probability with sigmoid `σ(z)=1/(1+e^(−z))`. A decision threshold such as 0.5 maps probability to a class, but calibration and class imbalance affect interpretation. For mutually exclusive multiple classes, softmax gives `p_k=e^(z_k)/sum_j e^(z_j)`. Logistic regression is a **classifier**, despite the name. These algorithm details were present in the repository before this update, but are not independently traceable to the uploaded four lecture decks.

**Bias/variance and model validation:** overly rigid models can underfit; overly flexible models can overfit. K-fold validation rotates training/validation folds, with all learned preprocessing fitted *within* each training fold. A final untouched test set is still valuable. For imbalanced categories, use an appropriate stratified strategy where supported.

## Regression metrics — supplemental explanation

`MAE = mean(|y−ŷ|)`, `MSE = mean((y−ŷ)^2)`, `RMSE=sqrt(MSE)`. MAE and RMSE retain the target units, while MSE has squared units and penalizes large errors more strongly. `R² = 1 − sum((y−ŷ)^2)/sum((y−mean(y))^2)` compares against a mean-target baseline and can be negative; handle constant targets carefully. These are general formulas, not measured results.

## Evidence status and use limits

The uploaded lecture mentions model selection and evaluation methods, but these notes do not claim independently executed model evaluations. No fabricated metrics or deployment results are presented.

## Sources
- Uploaded *Introduction to Machine Learning with Scikit-learn* lecture and practical worksheet.
- Existing repository classification page (pre-update), preserved and expanded as **supplemental** material.
