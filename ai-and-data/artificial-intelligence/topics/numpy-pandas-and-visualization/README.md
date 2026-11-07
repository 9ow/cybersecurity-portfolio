# NumPy, Pandas, and Matplotlib for Data Analysis

> **Sources:** uploaded *NumPy, Pandas, Matplotlib* lecture deck and practical worksheet. Code examples below are demonstrations/reconstructions of the taught API, not proof of completed personal lab exercises.

## NumPy: efficient numerical arrays

`numpy.ndarray` is a homogeneous, N-dimensional array. Compared with ordinary Python lists it supports consistent element types, compact storage, vectorized numerical operations and multidimensional indexing. `import numpy as np` is the lecture convention. Common array constructors are `np.array(values)`, `np.arange(start, stop, step)` (**stop excluded**), `np.linspace(start, stop, num)` (usually **includes endpoints**), `np.zeros(shape)`, and `np.ones(shape)`.

```python
import numpy as np
vector = np.array([10, 20, 30, 40, 50])
matrix = np.array([[1, 2, 3], [4, 5, 6]])
print(matrix.shape)  # (2, 3): rows, columns
print(matrix.size)   # 6 elements
print(matrix.ndim)   # 2 axes
print(matrix.dtype)  # Platform-dependent integer type
print(np.arange(0, 10, 2))   # [0 2 4 6 8]
print(np.linspace(0, 1, 5))  # [0.   0.25 0.5  0.75 1.  ]
```

Array methods `.sum()`, `.mean()`, `.min()`, `.max()`, `.argmin()`, `.argmax()`, and `.cumsum()` respectively give aggregation, mean, extremes, positions of extremes, and running totals. On `[10,20,30,40,50]`, the lecture reports sum 150, mean 30, argmin 0, argmax 4, cumulative totals `[10,30,60,100,150]`. `argmax` returns an **index**, not the maximum value.

**Indexing:** `vector[-1]` is the last item; `vector[1:4]` includes positions 1–3; `matrix[0,2]` is first row/third column; `matrix[:,1]` selects its second column. Boolean indexing `vector[vector > 30]` selects `40,50`. Slices can be views: assignments may affect the parent array; copies avoid that when independence is required.

## Broadcasting and vectorization

**Vectorization** applies arithmetic to whole arrays rather than explicit per-item Python loops. **Broadcasting** makes trailing dimensions compatible when dimensions match or one is 1. It does not mean *any* differently shaped arrays can be added: shapes `(2,3)` and `(3,)` work, but `(2,3)` and `(2,)` do not.

```python
a = np.array([[1, 2, 3], [4, 5, 6]])
b = np.array([10, 20, 30])
print(a + b)
# [[11 22 33]
#  [14 25 36]]
first = np.array([10, 20, 30, 40, 50])
second = np.array([1, 2, 3, 4, 5])
print(first + 6)        # [16 26 36 46 56]
print(first * second)   # [10 40 90 160 250]
print(first / second)   # [10. 10. 10. 10. 10.]
```

These arithmetic results are deterministic and correspond to the **worksheet's supplied sample output**; they are not presented as personal completion evidence. Array shape, compatible dtypes and division by zero need checking.

## Pseudorandom values and reproducibility

`np.random.rand(...)` samples floats on `[0,1)`, `np.random.randint(low, high, size=...)` chooses integer values with **exclusive `high`**, and `np.random.seed(42)` sets the legacy global RNG state so the same operation sequence is reproducible. The slides demonstrate sample random outputs; without fixing the exact seed and call order, those exact numbers are not guaranteed. Random samples are not cryptographically secure.

## Pandas: labeled data, CSV, selection, and modification

A **Series** is one-dimensional with an index; a **DataFrame** is a two-dimensional table whose columns can have different types. `pd.read_csv(path)` loads a CSV and `df.to_csv(path, index=False)` writes it without a separate index column. `head(n)`/`tail(n)` preview rows, `info()` prints counts and dtypes, and `describe()` summarizes numeric fields by default.

```python
import pandas as pd
df = pd.DataFrame({"Product": ["A", "B", "C"],
                   "Price": [10, 20, 30]})
print(df["Price"])                   # Select named column (Series)
print(df.iloc[0])                   # Row at integer position 0
print(df.loc[1, "Price"])           # Label 1, column Price
print(df[df["Price"] >= 20])        # Boolean filter
df["WithTax"] = df["Price"] * 1.10  # Vectorized new column
df = df.rename(columns={"Price": "BasePrice"})
df = df.drop(columns=["WithTax"])
```

`iloc` is **positional**, whereas `loc` uses **index labels**, including endpoints when slicing a label range. `df.loc[row_label, column]` can update a specific cell. The practical shows renaming, inserting a new row with `loc`, adjusting numeric columns with vectorized arithmetic, and combining tables with `pd.concat`. `drop` removes selected axes; `replace` substitutes specified values; carefully distinguish copies from `inplace` changes.

## Matplotlib: choosing the right chart

A **Figure** is the overall canvas; an **Axes** is a plotting region inside it, holding X and Y axes, data elements, title, labels and a legend. `plt.subplots()` returns both. Use a line chart (`plot`) for trends/ordered observations, bars (`bar`) for category counts, scatter (`scatter`) for relationships/outliers, and histogram (`hist(bins=...)`) for value distributions. Axis labels, units, comparable scales, clear titles, and honest bin choice affect interpretability.

```python
import matplotlib.pyplot as plt
import numpy as np
x = np.linspace(0, 10, 100)
y = np.sin(x)
fig, ax = plt.subplots()
ax.plot(x, y, label="sin(x)")
ax.set(title="Sine Function", xlabel="x", ylabel="sin(x)")
ax.grid(True)
ax.legend()
plt.show()
```

The lecture also uses `plt.bar(["Apples","Bananas","Cherries"], [10,15,7])`, `plt.scatter(x,y)`, `plt.hist(data,bins=30)`, and Pandas `df.plot(...)`. A scatter plot can suggest association, **not causal effect**; histograms change appearance with bin width; line charts can misleadingly imply continuity for unordered categories. In saved notebooks, plots should be labeled by what data generated them.

## Practical worksheet: separate exercises

The worksheet's NumPy practice requests scalar broadcasting and element-wise addition/subtraction/multiplication/division. The Pandas exercise provides an employee DataFrame and asks to add an increment, increase salaries 10%, rename `Employee`, drop `Department`, and replace one sample name. Avoid publishing that example as an actual employee dataset.

The visualization exercise specifies seven daily sales `[40,45,50,55,65,70,80]`, totals `[400,540,360]`, and seven advertising budgets versus units sold. The tasks request line, bar and scatter charts respectively; they are **instructions, not verified submitted plots**. No screenshots should be included.

## Sources
- Uploaded *NumPy, Pandas, Matplotlib* slides: ndarray creation, metadata, slicing, broadcasting, RNG, Series/DataFrame, chart anatomy and methods.
- Uploaded *NumPy, Pandas, and Matplotlib* worksheet: worked examples and three final practical prompts.
