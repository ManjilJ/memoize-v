# Memoization Visualizer 🧠✨

An interactive, animated web application designed to visually explain the concept of **memoization** using the classic Fibonacci sequence as an example. This tool helps developers and students understand how caching results of expensive function calls can dramatically improve performance.

### Link: https://manjilj.github.io/memoize-v/

---

## 🚀 Key Features

- ✨ **Dynamic Animations:** Watch as data flows between logical steps (checking the cache, executing a function, returning a result).
- ↔️ **Synchronized Code Highlighting:** The code block on the right highlights the exact line of logic being executed in the visualization, connecting the concept to the implementation.
- 📚 **Detailed Recursion View:** Toggle a special mode to see the call stack build and unwind in real-time. This view provides step-by-step insight into how the recursive `fib(n-1) + fib(n-2)` calls are resolved.
- 💾 **Live Cache Visualization:** The `Object (Cache)` box updates in real-time, clearly showing which values are being stored and retrieved.
- ⚡️ **Cache Hit vs. Miss:** The visualizer uses distinct colors and paths to clearly distinguish between fetching a pre-calculated value (a fast, green cache hit) and performing a new calculation (a "heavy," red function call).
- 🎛️ **Interactive Controls:** Input your own number for `n`, run the simulation, clear the cache, and toggle the detailed view on or off. Maximum allowed n is 31 when recursion details is toggled to be shown and 1477 when it is not.

---

## 📖 The Visualization Explained

The application breaks down the process of a memoized function call into a few simple, visual stages.

1.  **Start (Input):** You provide an integer `n` and click "Run".
2.  **1. Checking:** The first stop is to check if the result for `fib(n)` already exists in our `cache` object.
    - ✅ **Cache Hit:** If `n` is found in the cache, the flow is quick and efficient. A green path travels directly from the cache to the result box.
    - ❌ **Cache Miss:** If `n` is not in the cache, the flow is diverted. A red path travels to the "Heavy Function" box, indicating that a calculation is required.
3.  **2. Heavy Function:** This is where the actual Fibonacci calculation happens.
    - **Simple Mode:** A processing animation runs, and the result is computed quickly in the background.
    - **Recursion Detail Mode:** This is the most powerful view. The application pauses and steps through the recursive calls.
      - The **Call Stack** box shows which function calls are currently pending.
      - The **Recursion Details** monitor provides a play-by-play of the current state, showing base case hits (`n <= 1`), cache hits, and the resolution of `fib(n-1)` and `fib(n-2)`.
4.  **Object (Cache):** Once a new value is calculated, an animation shows it being stored in the `cache` object. The UI updates to reflect the new key-value pair.
5.  **3. Result Return:** Finally, the computed or retrieved value is delivered to the result box, completing the process.

By running the function multiple times or with overlapping recursive calls (like `fib(6)`), you can clearly see the power of memoization as more and more paths turn from red (calculate) to green (retrieve).


---
---

## What is the Fibonacci Sequence? 🔢

The Fibonacci sequence is one of the most famous sequences in mathematics. It is a series of numbers where each number is the sum of the two preceding ones.

### The Rules

The sequence is defined by a simple recursive relationship:

*   The first number, `fib(0)`, is **0**.
*   The second number, `fib(1)`, is **1**.
*   Every subsequent number is the sum of the two before it: `fib(n) = fib(n - 1) + fib(n - 2)`.

### The Sequence

Following these rules, the sequence begins:

**0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, ...**

Let's see how it's built:
*   `fib(2) = fib(1) + fib(0)`  => `1 + 0 = 1`
*   `fib(3) = fib(2) + fib(1)`  => `1 + 1 = 2`
*   `fib(4) = fib(3) + fib(2)`  => `2 + 1 = 3`
*   `fib(5) = fib(4) + fib(3)`  => `3 + 2 = 5`
*   ...and so on.


Shorter snippets of memoized versions of Fibonacci series

1. Longer version
```javascript
function memoizedFib() {
  let cache = {}; // The cache is "closed over" by the inner function
  return function fib(n) {
    if (n in cache) {
      return cache[n]; // Return cached result
    } else {
      if (n <= 1) return n;
      // Calculate, store the result in the cache, then return it
      cache[n] = fib(n - 1) + fib(n - 2);
      return cache[n];
    }
  }
}

```

2. Uses an arrow function, a ternary operator, and the logical nullish assignment (??=) operator. This stores the cache directly on the function object itself to avoid needing an extra variable or a wrapper function.

```javascript
const fib = n => fib[n] ??= n < 2 ? n : fib(n - 1) + fib(n - 2)
```
3. Creates a instance with its own private cache

```javascript
const memoFib = (c = [0, 1]) => f = n => c[n] ??= f(n - 1) + f(n - 2)
```


This pattern is not just a mathematical curiosity; it famously appears in various aspects of nature, from the branching of trees and the arrangement of leaves on a stem to the fruitlets of a pineapple and the flowering of an artichoke.
