# Python: Simple Demo — TryHackMe

**Status:** Completed  
**Platform:** TryHackMe  
**Room:** [Python: Simple Demo](https://tryhackme.com/)  
**Focus:** Python fundamentals through an interactive number-guessing program.

## Objective

Build a command-line program that selects a secret integer between 1 and 20, accepts guesses, reports whether each guess is too low or too high, and counts attempts until the correct answer.

## 1. Random numbers and variables

```python
import random

secret = random.randint(1, 20)
tries = 0
guess = 0

print("I'm thinking of a number between 1 and 20")
```

- `import random` loads Python's random-number module.
- `random.randint(1, 20)` selects an integer including both endpoints.
- `secret` stores the selected number; `guess` holds the latest input; `tries` counts attempts.
- Initializing `guess` to 0 ensures it does not equal any valid secret at the start.

## 2. Input and type conversion

```python
text = input("Take a guess: ")
guess = int(text)
tries = tries + 1
```

`input()` returns a string even when the user types digits. `int()` converts numeric text to an integer so it can be compared with `secret`. The attempt counter increases after a guess is entered.

**Limitation:** Non-numeric input raises `ValueError` in this introductory version.

## 3. Conditional decisions

```python
if guess < 1 or guess > 20:
    print("That number is out of range. Try again.")
elif guess < secret:
    print("Too low, try again.")
elif guess > secret:
    print("Too high, try again.")
else:
    print("You got it in", tries, "tries!")
```

Python evaluates these branches in order and runs the first matching branch. The `or` operator checks whether either boundary is violated. The final `else` applies when the guess is within range and neither less than nor greater than the secret, so it must be equal.

## 4. Repetition with a while loop

The one-attempt version provides feedback but stops immediately. A `while` loop repeats the input and decision logic until the guess matches the secret.

### Complete example

```python
import random

secret = random.randint(1, 20)
tries = 0
guess = 0

print("I'm thinking of a number between 1 and 20")

while guess != secret:
    text = input("Take a guess: ")
    guess = int(text)
    tries = tries + 1

    if guess < 1 or guess > 20:
        print("That number is out of range. Try again.")
    elif guess < secret:
        print("Too low, try again.")
    elif guess > secret:
        print("Too high, try again.")
    else:
        print("You got it in", tries, "tries!")
```

**Indentation matters:** The `if / elif / else` block belongs **inside** the `while` block. If placed outside, the program keeps asking for guesses without giving feedback until the correct number is entered.

### Example interaction

```text
I'm thinking of a number between 1 and 20
Take a guess: 10
Too high, try again.
Take a guess: 5
Too low, try again.
Take a guess: 7
Too low, try again.
Take a guess: 8
You got it in 4 tries!
```

The transcript illustrates a run where the secret was 8; the actual number changes between executions.

## 5. Concepts reinforced

| Concept | Application |
| --- | --- |
| Variables | Maintain the secret, latest guess, and attempt count |
| Modules | Import `random` |
| Functions | Use `randint()`, `print()`, `input()`, and `int()` |
| Comparisons | Evaluate `<`, `>`, and `!=` |
| Boolean logic | Reject out-of-range input with `or` |
| Conditionals | Choose the appropriate hint with `if / elif / else` |
| Loops | Continue prompting with `while` |
| Indentation | Control which statements execute during each iteration |

## Limitations and possible improvements

This is an introductory implementation, not a hardened input-processing utility. Non-numeric input is not handled, and out-of-range guesses still increment the attempt counter. A future iteration could validate input using `try / except` and decide whether invalid attempts should count.

## Security relevance

The same Python building blocks support defensive automation: reading input, validating ranges, applying decision rules, tracking counts, and repeating checks. This exercise demonstrates those programming fundamentals; it is not presented as a completed security tool.

**Documentation format:** Code and explanations only; no screenshots.
