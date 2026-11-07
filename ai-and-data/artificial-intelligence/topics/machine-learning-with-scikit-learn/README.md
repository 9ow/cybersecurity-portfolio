# Machine Learning and Scikit-learn

> **Sources:** uploaded *Introduction to Machine Learning with Scikit-learn* lecture and associated practical worksheet. Distinguish teaching examples from trained, measured personal models.

## Machine learning vs. programmed rules

A traditional program implements rules written by humans. A machine-learning **algorithm** estimates parameters or patterns from labeled or unlabeled observations; a trained **model** is the result of that fitting process. The lecture highlights spam detection, medical image classification, predictive maintenance, personalized recommendations, autonomous systems and forecasting. A model needs a clearly defined objective and representative data: strong performance on training examples alone cannot establish **generalization** to previously unseen data.

The lecture sketches a workflow: define the task → collect/inspect data → visualize → preprocess → train → evaluate → obtain feedback/refine → predict, potentially deploy. This is a **conceptual lifecycle**, not a record that deployment occurred.

## Learning paradigms and problem framing

- **Supervised learning:** features `X` and known targets `y`. **Classification** predicts discrete categories (for example spam/not spam or flower species); **regression** predicts a numeric quantity (such as a bill or journey duration).
- **Unsupervised learning:** features but no target labels; explore clusters/associations, exemplified in the lecture by grouping observations by color. The practical points to K-Means, DBSCAN and hierarchical clustering in scikit-learn documentation but does not walk through training them.
- **Reinforcement** and **semi-supervised** learning are mentioned as additional paradigms, not taught with completed algorithms.

A row is an observation and a column is a feature or target. Define which column is being predicted **before** constructing `X`: including the target in `X` leaks the answer. Predicting among several named categories is **multiclass supervised classification**, not regression merely because labels are encoded as integers.

## Scikit-learn's consistent API

Scikit-learn provides `sklearn.datasets` toy data (`load_iris`, `load_diabetes`, `load_digits`, `load_breast_cancer`, etc.), `model_selection`, `preprocessing`, and supervised/unsupervised estimators. A returned dataset typically offers `.data`, `.target`, `.feature_names`, and sometimes `.target_names`. Do not assume every dataset, especially a regression dataset, defines class names.

```python
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler

iris = load_iris()
X, y = iris.data, iris.target
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.20, random_state=42, stratify=y
)
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)  # Do NOT fit on test
```

**Parameters:** `test_size=0.20` reserves 20% for testing; `train_size` can specify training share; `random_state` fixes the pseudorandom split; `shuffle` controls mixing; `stratify=y` (additional project-context option) approximately preserves class proportions when possible. `fit` learns from the training split; `transform` applies learned preprocessing, `fit_transform` combines them. MinMax scaling uses `(x-min)/(max-min)` per training feature for range `[0,1]`; standardization uses `z=(x-mean)/standard_deviation`. Constant features need special handling; numerical transformations do not fix semantic errors.

`LabelEncoder` maps **target labels** to integer IDs. Integer codes do **not** imply class ranking. `OneHotEncoder` is appropriate for nominal input categories when a model should not interpret category codes as distances; `ColumnTransformer` assigns transformations by columns and `SimpleImputer` fills missing values with a chosen statistic. Fit all learned transformations only on training examples to avoid evaluation leakage.

## Worked rules: arithmetic is not fitted-model evidence

In the lecture's profit example, observed sales `30,40,50,70` map to profits `3,4,5,7`, illustrating **y = 0.1X**; for `X=100`, predicted profit is `10` in the prescribed example. For electricity charges the **supplied** rule is `y = 10 + 0.15X` BHD, so 250 units yield **47.5 BHD**. The travel-time worksheet specifies `time = distance/speed`; 260 km at 70 km/h gives **26/7 ≈ 3.714 hours**, assuming constant average speed. These are calculations using supplied equations, **not outputs from an executed fitted estimator**.

## Practical worksheet: taught operations versus results

The worksheet points to scikit-learn's User Guide, toy datasets, preprocessing and supervised/unsupervised reference pages. Its screenshots **illustrate** loading Iris, a 120/30 split for Iris at 80/20, scaling via `MinMaxScaler`, and encoding categorical fruit labels. Final exercises request inspecting `load_diabetes()`, splitting it 70/30, applying `StandardScaler` to training data, and solving the travel-time arithmetic example. The diabetes regression target does not inherently have categorical `target_names`; inspect the object and report absence instead of inventing labels.

**Evidence status:** uploaded lecture/worksheet demonstrations do not establish that a personal classifier or regression model was fit, evaluated or deployed. Future results should record exact train/test division, random seed, preprocessing, training code, metric and observed output, with no private data.

## Sources
- Uploaded *Introduction to Machine Learning with Scikit-learn* PPT: definitions, paradigms, datasets, splitting, preprocessing and worked equations.
- Uploaded *Introduction to Machine Learning with Scikit-learn* worksheet: navigation, Iris examples, diabetes practice, distance/speed exercise.
