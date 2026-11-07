# Data Quality, Cleaning, and Preprocessing

> **Sources:** uploaded *Data Cleaning* lecture and *Cleaning Datasets* worksheet.

## Why data quality changes conclusions

The lecture describes data cleaning as detecting and correcting incomplete records, duplicates, inconsistent labels, wrong data types, redundant features and extreme observations. Cleaning can change sample size, class balance and what the model can learn. Never assume every unusual record is erroneous or that dropping rows is harmless. Inspect before changing; report the rules and the number of affected records.

## Missing values: detection, deletion, imputation

`df.isnull().sum()` counts missing values **by column**; `df.isna().any(axis=1).sum()` counts rows with at least one missing value; `df.info()` shows non-null counts and types. `dropna()` normally drops rows with any missing value; `dropna(axis=1)` drops columns. Applying both sequentially is often unnecessarily destructive. Mean imputation is easy for numeric values but sensitive to outliers; median resists extremes; mode fills with the most common observed value for numeric or categorical data. A fully missing column cannot be filled from its own mean/mode without an alternative policy.

```python
import pandas as pd
df = pd.read_csv("data.csv")
print(df.isna().sum())
print(df.isna().any(axis=1).sum())
numeric = df.select_dtypes(include="number").columns
filled = df.copy()
filled[numeric] = filled[numeric].fillna(filled[numeric].median())
```

For model evaluation, compute imputation statistics using **training data only**, and apply them unchanged to test data. `SimpleImputer(strategy="mean"|"median"|"most_frequent")` is the scikit-learn counterpart introduced in the ML lecture.

## Duplicates, category labels, types, and feature selection

`df.duplicated().sum()` counts repeated **entire rows** (excluding their first occurrence by default); `df.drop_duplicates()` retains the first. In some domains two identical transactions or traffic observations may be legitimate, so confirm the record definition. Standardize text with `.str.strip()` and `.str.upper()` or a vetted mapping, avoiding changes to semantically distinct classes. Numeric strings can be converted by `pd.to_numeric(..., errors="coerce")` after investigating bad tokens; dates by `pd.to_datetime(...)` with an explicit format where feasible. Converting invalid values to `NaN` silently and then dropping them can conceal data-quality problems—report the number.

Remove identifiers that are not meaningful predictive features, but do not remove informative rare indicators merely because their variance is small. A feature that is constant for **all observations** carries no discrimination in that dataset. Two exactly identical features duplicate information. Highly correlated does not always mean interchangeable.

## Encoding and numerical scaling

`LabelEncoder` assigns integer IDs to a target class; **nominal feature** categories are commonly one-hot encoded (`pd.get_dummies` or `OneHotEncoder`). A numeric category code does not imply a ranked order. `StandardScaler` learns training mean and standard deviation and applies `z=(x-μ)/σ`; `MinMaxScaler` uses training extrema. Fit on train, transform test, to prevent data leakage.

## Outliers: understand IQR before choosing an action

The lecture uses quartiles `Q1=25th percentile`, `Q3=75th percentile`, **IQR = Q3 − Q1**, with fences **lower = Q1 − 1.5×IQR** and **upper = Q3 + 1.5×IQR**. For example if `Q1=10`, `Q3=18`, `IQR=8`; fences are `-2` and `30`. Values outside are **flags**, not automatically mistakes. The technical reference's salary example flags extreme values compared with ordinary salaries, but legitimate extreme observations can occur in many domains. Keep/drop/clip decisions should have domain justification and be fitted without peeking at the test split.

```python
q1 = df["numeric_feature"].quantile(0.25)
q3 = df["numeric_feature"].quantile(0.75)
iqr = q3 - q1
flagged = df[(df["numeric_feature"] < q1 - 1.5 * iqr) |
             (df["numeric_feature"] > q3 + 1.5 * iqr)]
```

## Worksheet tasks (assigned; not verified personal execution)

The cleaning practical illustrates file upload in Colab, `isnull`/`info`, removing missing rows, mean and mode imputation, duplicate removal and encoding. Its final **employee dataset** task asks for deduplication, mean imputation of Age and Salary, Gender encoding, and Salary IQR inspection. The **healthcare dataset** task requests duplicate-patient checks, mean imputation of Blood_Pressure and BMI, encoding Diagnosis and Gender, and investigation of ages greater than 100. Those example datasets and executed submissions are **not** among the uploaded verification evidence; no results are claimed. Exclude patient data and identifiable employee details from GitHub.

## Sources
- Uploaded *Data Cleaning* technical materials: data quality, imputation, duplicates, text normalization, dtype changes, feature selection, encoding, boxplots/IQR.
- Uploaded *Cleaning Datasets* practical worksheet: demonstrated procedures and assigned employee/healthcare tasks.
