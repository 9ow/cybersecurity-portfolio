# Artificial Intelligence and Python Programming Foundations

> **Source provenance:** *Overview of AI & Python Fundamentals* lecture slides and *Introduction to Python Programming* practical worksheet. This page explains lecture concepts and supplies illustrative code, **not** evidence of independently completed worksheet submissions.

## Artificial intelligence: approaches, foundations, and scope

The lecture distinguishes four approaches: **thinking humanly** (model human cognition), **thinking rationally** (formal logical reasoning), **acting humanly** (observable human-like behavior), and **acting rationally** (choose actions that best achieve an objective). These are different definitions rather than interchangeable model-training algorithms. A rational agent may act effectively without thinking like a person.

The slides connect AI to mathematics (linear algebra, probability/statistics, calculus and optimization), computing/programming, data quality, machine learning, neural networks/deep learning, search and reasoning, NLP, computer vision, robotics/control, and responsible AI. Applications include spam filtering, speech recognition, games, automated planning and robotic vehicles. **Machine learning** learns patterns from examples, while rule-based systems execute programmer-specified logic. **Deep learning** is a subset of ML using multilayer neural networks; the overview does not teach how to train one.

## Input, output, values, and conversion

Python is a readable, interpreted general-purpose language. `input(prompt)` returns a **string** even when digits were entered; `int()` and `float()` explicitly convert it, and invalid text raises `ValueError`. `print(*objects, sep=" ", end="\n")` controls separators and line endings; its other worksheet parameters are `file` (output stream) and `flush` (force a write). `type()` inspects the resulting value.

| Type | Meaning | Example | Important limit |
| --- | --- | --- | --- |
| `int` | Whole number | `25` | Not the same as text `"25"` |
| `float` | Floating-point numeric value | `2.5` | Binary rounding can affect decimal comparisons |
| `complex` | Real and imaginary components | `2+3j` | The imaginary suffix in Python is `j` |
| `str` | Immutable Unicode text | `"AI"` | Cannot assign to an individual character |
| `bool` | Logical truth value | `False` | Conditions evaluate truth values |
| `bytes`, `bytearray` | Byte sequences | `b"AI"` | Bytes restricted to 0–255; bytearray is mutable |

```python
raw_age = input("Enter an age: ")
age = int(raw_age)
print("Next year:", age + 1)
print(type(raw_age), type(age))  # str, int
```

**Lecture activity:** classify `25`, `"25"`, `2.5`, and `False` as integer, string, float, and Boolean. Another activity asks for name and age and prints a greeting after converting the age. The examples are illustrative, not records of personal execution.

## Conditionals, loops, and program flow

Indentation defines Python blocks. `if` checks a condition; `elif` checks the next condition **only if** earlier branches failed; `else` is the fallback. A `for` loop traverses elements or `range`; `while` repeats while its condition stays true, so update its state to avoid infinite loops.

```python
temperature = 25
if temperature > 30:
    print("Hot")
elif temperature > 20:
    print("Warm")  # This branch applies
else:
    print("Cold")

for n in range(5):  # 0, 1, 2, 3, 4
    if n == 2:
        continue  # Skip only this iteration
    if n == 4:
        break     # Exit loop
    print(n)
```

`pass` deliberately does nothing and is appropriate as a temporary placeholder. Unlike `continue`, it does **not** skip printing or other code afterward. The slides contain a few conflicting comments (for example a comment describing an even-number skip when the code skips only `5`); trust the actual condition and trace it.

## Strings: indices, slicing, and transformations

Strings are immutable sequences indexed from zero; `-1` means the last character. `text[start:stop:step]` excludes `stop`; `[::-1]` reverses. Useful methods: `.lower()`, `.upper()`, `.strip()`, `.replace(old,new)`, `.find(substring)` (returns `-1` when absent), and `.split(delimiter)` (returns a list). Methods typically return a new string rather than mutating the original.

```python
text = "  Python Programming  "
clean = text.strip()
print(clean[:6])       # Python
print(clean[::-1])     # gnimmargorP nohtyP
print(clean.split())   # ['Python', 'Programming']
```

**Worksheet exercise:** for even-length text print the first half; otherwise print its middle character. The condition is `len(s) % 2 == 0`, the first half `s[:len(s)//2]`, and the odd middle `s[len(s)//2]`. Whether spaces count depends on whether the program removes them first.

## Functions, imports, and local scope

`def` defines reusable logic; parameters accept inputs and `return` provides a value. Without `return`, a function returns `None`. Locally assigned variables are normally not available outside the function. Modules are `.py` files that organize definitions; examples use `math.sqrt`, `math.factorial`, `random.randint` and `datetime.date.today`. An alias such as `import math as m` changes only how the module is referenced.

```python
def add(a, b):
    return a + b

import math as m
print(add(3, 4))    # 7
print(m.factorial(5))  # 120
```

## Collections and methods

| Collection | Order/structure | Mutability | Duplicates | Representative operations |
| --- | --- | --- | --- | --- |
| List `[...]` | Indexed sequence | Mutable | Allowed | `append`, `extend`, `insert`, `remove`, `pop`, `count`, `index`, `reverse`, `copy`, `clear` |
| Tuple `(...)` | Indexed sequence | Immutable | Allowed | `count`, `index`, `len`, `min`, `max` |
| Dictionary `{key:value}` | Insertion-ordered mapping in modern Python | Mutable | Keys unique | `get`, `keys`, `values`, `items`, `pop`, `popitem`, `copy`, `clear`, `fromkeys` |
| Set `{...}` | Unordered unique elements | Mutable | Not allowed | `add`, `discard`, `union`, `intersection`, `difference`, `update`, `clear` |

`list.remove(x)` removes the first matching value (and raises an error when absent); `pop(i)` returns and removes the chosen element (last by default). `list.reverse()` modifies the list **in place**; the slide's illustrated output after reversing appears inconsistent with its stated operation. Dictionary `get(key, default)` differs from `fromkeys(keys, value)`; one accesses a key and the other creates a dictionary. Sets cannot be accessed with positional indexing, and `set.pop()` removes an arbitrary member rather than a guaranteed first or last one.

## Practical worksheet: assigned work, not execution evidence

The worksheet introduces Colab/Jupyter setup, output formatting and interactive input, checking types, branching and repetition, slicing, function calls, module imports, and collections. Its four final prompts are: extract half/middle of input text; implement `rem_dups(temp)` preserving unique values; count words in a sentence; and select tuple values above their average. Their displayed *sample outputs* are worksheet examples, **not personally verified runs**. A simple order-preserving solution to the second prompt is:

```python
def rem_dups(temp):
    result = []
    for item in temp:
        if item not in result:
            result.append(item)
    return result
```

**Evidence boundary:** no uploaded executed Python notebook proves these lab tasks were completed. Keep future personal code, inputs, console output and troubleshooting in text, without private identifiers or screenshots.

## Sources
- Uploaded *Overview of AI & Python Fundamentals* slide deck: AI approaches, foundations, types, control flow, strings, functions, modules, collections.
- Uploaded *Introduction to Python Programming* worksheet: Colab instructions, `print` parameters, exercises and sample outputs.
