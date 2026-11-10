# JavaScript: Simple Demo — TryHackMe

**Status:** Completed  
**Platform:** TryHackMe  
**Focus:** JavaScript fundamentals and a command-line number-guessing game using Node.js.

## Overview

Implemented the same number-guessing concept introduced in the Python: Simple Demo room to compare language syntax and execution. The program selects a secret integer from 1 to 20, accepts guesses, reports whether they are too high or too low, and repeats until the user finds the number.

JavaScript can execute in a browser's developer console or outside a browser with Node.js. This exercise uses Node.js.

## 1. Variables and constants

```javascript
let tries = 0;
let guess = 0;
const secret = Math.floor(Math.random() * 20) + 1;
```

- `let` declares variables that can be reassigned.
- `const` prevents reassignment of the secret number during a run.
- `Math.random()` returns a number from 0 (inclusive) to 1 (exclusive).
- Multiplying by 20, rounding down with `Math.floor()`, and adding 1 produces an integer from 1 to 20.

## 2. Console output and user input

```javascript
console.log("I'm thinking of a number between 1 and 20");

const text = await rl.question("Take a guess: ");
guess = parseInt(text, 10);
tries = tries + 1;
```

`console.log()` displays output. `rl.question()` waits for input and returns text; `parseInt(text, 10)` interprets it as a base-10 integer. The attempt counter increases after each entry.

The `rl` object must be initialized using Node.js's `readline/promises` interface before asking questions.

## 3. Conditional feedback

```javascript
if (guess < 1 || guess > 20) {
    console.log("That number is out of range. Try again.");
} else if (guess < secret) {
    console.log("Too low, try again.");
} else if (guess > secret) {
    console.log("Too high, try again.");
} else {
    console.log("You got it in", tries, "tries!");
}
```

The `||` operator means logical OR. Only the first matching `if / else if / else` branch executes. The initial version (`guess_v2.js`) evaluated just one guess before exiting.

## 4. Complete program — guess_v3.js

```javascript
import * as readline from "node:readline/promises";
import { stdin as input, stdout as output } from "node:process";

const rl = readline.createInterface({ input, output });

try {
    const secret = Math.floor(Math.random() * 20) + 1;
    let tries = 0;
    let guess = 0;

    console.log("I'm thinking of a number between 1 and 20");

    while (guess !== secret) {
        const text = await rl.question("Take a guess: ");
        guess = parseInt(text, 10);
        tries = tries + 1;

        if (guess < 1 || guess > 20) {
            console.log("That number is out of range. Try again.");
        } else if (guess < secret) {
            console.log("Too low, try again.");
        } else if (guess > secret) {
            console.log("Too high, try again.");
        } else {
            console.log("You got it in", tries, "tries!");
        }
    }
} finally {
    rl.close();
}
```

The `while (guess !== secret)` condition keeps the program running until the guess strictly equals the secret. All input, conversion, counting, and feedback statements must remain inside the loop. The `finally` block closes the input interface.

### Running with Node.js

Save the code as `guess_v3.js` and execute it with a recent Node.js version that supports ECMAScript modules and top-level `await`:

```bash
node guess_v3.js
```

If your Node.js environment does not treat `.js` as an ECMAScript module, use `guess_v3.mjs` instead and run `node guess_v3.mjs`.

### Example interaction

```text
I'm thinking of a number between 1 and 20
Take a guess: 10
Too low, try again.
Take a guess: 15
Too high, try again.
Take a guess: 13
Too low, try again.
Take a guess: 14
You got it in 4 tries!
```

This example represents a run where the secret is 14; the selected value changes between runs.

## 5. Python and JavaScript comparison

| Concept | Python | JavaScript |
| --- | --- | --- |
| Mutable variable | `tries = 0` | `let tries = 0;` |
| Output | `print("Hello")` | `console.log("Hello");` |
| String to integer | `int(text)` | `parseInt(text, 10)` |
| Random integer 1–20 | `random.randint(1, 20)` | `Math.floor(Math.random() * 20) + 1` |
| Loop until equal | `while guess != secret:` | `while (guess !== secret) {` |
| Code blocks | Indentation | Braces `{ }` |

## 6. Limitations and security relevance

The exercise demonstrates input handling, control flow, and repeated decision-making—fundamentals useful for automation and web application security analysis. It is not a security assessment tool.

**Input-validation limitation:** `parseInt("hello", 10)` produces `NaN`. Because comparisons such as `NaN < secret` and `NaN > secret` are false, the example's final `else` incorrectly prints success. The `while` condition remains true, so it then prompts again. A stronger implementation would check `Number.isNaN(guess)` and validate that input is an integer in the expected range before comparing it with the secret.

**Documentation:** Code and technical explanation only; no images.
