# Support Vector Machines: Decision Boundaries and Margins

> **Evidence boundary:** The existing repository already contained an SVM explanation. The four uploaded lecture decks and their worksheets only **mention SVM as an example of a supervised estimator or scikit-learn documentation topic**; they do not supply a dedicated SVM lesson, experiment, classifier performance, or fitted output. The deeper sections below are retained and clarified as **supplemental technical reference**, not attributed to unseen technical materials.

## Linear separating hyperplanes

An SVM classifier learns a decision boundary, often written `w·x+b=0`. In two features it is a line; in `d` features it is a hyperplane. For a new observation `x`, the sign of `f(x)=w·x+b` chooses the side of the boundary for a binary linear classifier. The geometrically closest training points that constrain the boundary are **support vectors**. Feature units strongly affect the geometry, so scaling is commonly important.

## Margin and optimization

For separable binary labels `y_i∈{-1,+1}`, a canonical hard-margin problem is: minimize `1/2 ||w||²`, subject to `y_i(w·x_i+b)≥1` for every training example. The resulting full margin width is `2/||w||`. When classes overlap, **soft margin** allows violations via slack `ξ_i≥0`: minimize `1/2||w||²+C Σ_i ξ_i` subject to `y_i(w·x_i+b)≥1−ξ_i`. Higher `C` penalizes training violations more; it is not a guarantee of stronger test performance.

## Kernels and nonlinear separation

A kernel calculates feature-space similarity without explicitly forming high-dimensional vectors. The commonly used radial basis function (RBF) kernel is `K(x,z)=exp(−γ||x−z||²)`. Larger `γ` generally makes similarity shrink more rapidly with distance and can yield more local boundaries. A curved decision boundary in original coordinates is possible, but also risks overfitting when tuning `C` and `γ`. Different kernels encode different assumptions and costs.

## Scikit-learn example — teaching-only, not executed evidence

```python
from sklearn.pipeline import make_pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.svm import SVC

# X_train and y_train must be prepared from a verified training split.
classifier = make_pipeline(
    StandardScaler(),
    SVC(kernel="rbf", C=1.0, gamma="scale")
)
# classifier.fit(X_train, y_train)
# labels = classifier.predict(X_test)
```

`SVC` offers `kernel` (such as `linear` or `rbf`), `C` (regularization trade-off), and `gamma` (RBF/poly/sigmoid kernel coefficient). `gamma="scale"` chooses a data-dependent value. Fitting and evaluating this pipeline were **not performed or claimed** here. `decision_function` gives signed scores/margins for binary classification; raw scores are **not** calibrated probabilities. Multi-class SVC commonly fits pairwise decision boundaries, which complicates direct score interpretation. Nonlinear-kernel SVMs can become computationally costly on large datasets.

## Use cases, limitations and evaluation

SVMs can work well for moderate-size numerical feature datasets, particularly with appropriate scaling. They may be less suitable for extremely large datasets or require careful hyperparameter selection. Rare classes and class imbalance complicate evaluation; use per-class metrics and preserve an unseen test set. Explain cross-validation and actual results only after executable evidence is available. The old repository's email Work/Personal illustration is a conceptual example, **not** a completed case study.

## Sources
- Uploaded *Introduction to Machine Learning with Scikit-learn* technical materials/worksheet: SVM name appears in lists of supervised-learning approaches, without algorithm detail.
- Existing repository *Support Vector Machines* article: conceptual reference present before this revision; enhanced here as explicitly marked supplemental background.
