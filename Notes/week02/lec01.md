# Lecture 1: Analysis of Algorithms

> **Course:** Design and Analysis of Algorithms (DAA)
> **Lecture Duration:** ~35 minutes
> **Topic:** Introduction to Algorithm Analysis and Time Complexity

---

# Why Study Algorithm Analysis?

Designing an algorithm is only the first step. We also need to determine **how efficient** it is.

Algorithm analysis helps answer the following questions:

* How long will the algorithm take to execute?
* How much memory will it require?
* Will it remain practical when the input size becomes very large?

The lecture begins with the Aadhaar–SIM verification example to demonstrate that a clever algorithm can reduce execution time from **thousands of years to just a few minutes**, highlighting why algorithm analysis is essential.

---

# Performance Measures

## 1. Time Complexity

Time complexity measures the amount of time an algorithm takes to execute.

Example:

* Aadhaar–SIM verification
* Sorting
* Searching

Time complexity is the primary focus because execution time determines whether an algorithm is practical.

---

## 2. Space Complexity

Space complexity measures the extra memory required during execution.

Examples:

* Temporary arrays
* Variables
* Auxiliary data structures

> **Note:** Memory is usually easier to upgrade than CPU performance. Therefore, this course focuses mainly on **time complexity**.

---

# Hardware vs Algorithm

A faster computer does **not** compensate for an inefficient algorithm.

Even upgrading to a processor that is **10× faster** only gives a constant-factor improvement.

However, improving the algorithm itself (for example, from **O(n²)** to **O(n log n)**) can reduce execution time from **years to seconds**.

**Key Idea:**

> Good algorithms are more valuable than powerful hardware.

---

# Naive vs Efficient Algorithm

## Problem

Verify whether every SIM card is linked to a valid Aadhaar number.

---

## Naive Approach

For every SIM card:

* Compare it with every Aadhaar number.

Pseudo-logic:

```text
for each SIM card
    compare with every Aadhaar card
```

If there are **n** SIM cards and **n** Aadhaar cards,

$$
T(n)=n^2
$$

because of two nested loops.

For one billion records, this approach would require **thousands of years**.

---

## Efficient Approach

First sort the Aadhaar database.

Then search every Aadhaar number using **Binary Search**.

Binary Search repeatedly halves the search space.

Each search takes

$$
\log_2 n
$$

There are **n** SIM cards.

Therefore,

$$
T(n)=n\log n
$$

This reduces execution time dramatically—from **thousands of years** to only **a few minutes**.

---

# Running Time Depends on Input Size

The execution time of an algorithm depends primarily on the **input size**.

Examples:

* Larger arrays require more sorting time.
* Larger lists require more searching time.
* Larger graphs require more processing.

Running time is represented as

$$
T(n)
$$

where

* **T(n)** = Running time
* **n** = Input size

The goal of algorithm analysis is to study how **T(n)** grows as **n** increases.

---

# Same Input Size Does Not Mean Same Running Time

Even when the input size is fixed, different inputs may require different amounts of work.

Example:

Searching in an array.

### Easy Case

Target is the first element.

### Difficult Case

Target is absent.

Therefore,

same input size ≠ same running time.

---

# Closest Pair Problem (Video Game Example)

Suppose a game contains **100,000 objects**.

The game engine must continuously determine the **closest pair of objects**.

---

## Naive Solution

Compare every object with every other object.

Number of comparisons:

$$
\frac{n(n-1)}{2}
$$

which is approximately

$$
O(n^2)
$$

For

$$
n=10^5
$$

Operations:

$$
10^{10}
$$

Execution Time:

* Python → ~16 minutes
* C++ → ~1.6 minutes

Clearly impossible for a real-time game.

---

## Efficient Solution

An algorithm exists with complexity

$$
O(n\log n)
$$

Operations:

Approximately

$$
2\times10^6
$$

Execution Time:

* Python → ~0.2 seconds
* C++ → ~0.02 seconds

This is fast enough for real-time gameplay.

---

# Why We Ignore Constants

Consider

$$
5000n^2
$$

and

$$
n^3
$$

Initially,

$$
5000n^2
$$

may be larger.

However, as

$$
n\rightarrow\infty
$$

the cubic term eventually dominates.

Therefore,

$$
5000n^2<n^3
$$

for sufficiently large values of **n**.

Hence, in asymptotic analysis, **constant factors are ignored**.

---

# Asymptotic Analysis

Rather than studying small inputs,

we study algorithm behaviour when

$$
n\rightarrow\infty
$$

This is called **asymptotic analysis**.

Asymptotic analysis focuses on the growth rate of an algorithm rather than exact execution time.

---

# Common Time Complexities

| Complexity     | Description  | Example                      |
| -------------- | ------------ | ---------------------------- |
| **O(log n)**   | Logarithmic  | Binary Search                |
| **O(n)**       | Linear       | Linear Search                |
| **O(n log n)** | Linearithmic | Efficient Sorting            |
| **O(n²)**      | Quadratic    | Nested Loops                 |
| **O(n³)**      | Cubic        | Triple Nested Loops          |
| **O(2ⁿ)**      | Exponential  | Enumerating all subsets      |
| **O(n!)**      | Factorial    | Enumerating all permutations |

---

# Practical Feasibility

Approximate limits for modern computers.

| Complexity | Practical Input Size |
| ---------- | -------------------- |
| O(log n)   | Extremely large      |
| O(n)       | Millions             |
| O(n log n) | Millions             |
| O(n²)      | Around 10⁴–10⁵       |
| O(n³)      | Around 10³           |
| O(2ⁿ)      | Less than 100        |
| O(n!)      | Less than 15–20      |

Higher complexity algorithms become infeasible very quickly.

---

# Measuring Running Time

Instead of measuring seconds,

we count **basic operations**.

Examples:

* Assignment
* Comparison
* Arithmetic operation

This makes algorithm analysis independent of:

* Programming language
* Compiler
* Hardware

---

# Measuring Input Size

Different problems have different notions of input size.

### Arrays

Input size = Number of elements.

---

### Graphs

Input size consists of:

* Number of vertices (V)
* Number of edges (E)

Both affect algorithm performance.

---

### Numerical Problems

For numbers,

the input size is **not** the numerical value.

Instead,

it is the **number of digits (or bits)**.

Example:

Checking whether

```
387
```

is prime does **not** depend directly on 387,

but on the number of digits used to represent it.

---

# Best, Average and Worst Case Analysis

## Best Case

Minimum execution time.

Example:

Searching for the first element.

---

## Average Case

Expected running time across all possible inputs.

Although desirable,

average-case analysis is difficult because:

* Every possible input must be considered.
* A probability distribution over all inputs is required.

Therefore,

average-case analysis is rarely performed.

---

## Worst Case

Maximum execution time.

Example:

Searching for an element that is **not present** in a list.

Worst-case analysis is preferred because it provides a guaranteed upper bound on running time.

---

# Key Takeaways

* Algorithm performance is measured primarily using **time complexity**.
* Running time is expressed as a function **T(n)**.
* The efficiency of an algorithm depends on how quickly **T(n)** grows.
* Constant factors are ignored in asymptotic analysis.
* Efficient algorithms are more valuable than faster hardware.
* **O(n log n)** algorithms are generally practical for very large inputs.
* Exponential and factorial algorithms become impractical even for moderate input sizes.
* Worst-case analysis is the standard approach used in algorithm design.

---

# Important Formulae

### Linear

$$
O(n)
$$

### Logarithmic

$$
O(\log n)
$$

### Linearithmic

$$
O(n\log n)
$$

### Quadratic

$$
O(n^2)
$$

### Cubic

$$
O(n^3)
$$

### Exponential

$$
O(2^n)
$$

### Factorial

$$
O(n!)
$$

---

# GATE / Interview Focus

## Must Remember

* Time Complexity measures **growth of running time**, not actual execution time.
* Space Complexity measures **extra memory usage**.
* Ignore **constant factors** in asymptotic analysis.
* Binary Search has complexity **O(log n)** because the search space is halved after every comparison.
* **O(n log n)** algorithms are generally considered efficient for large datasets.
* Hardware improvements provide only constant-factor speedups; algorithmic improvements provide asymptotic improvements.
* Worst-case analysis is preferred because it guarantees an upper bound.

---

# Common GATE Questions

### Q1. Why is Binary Search **O(log n)**?

**Answer:**
Each comparison reduces the search space by half. Therefore, the number of comparisons required is proportional to $\log_2 n$.

---

### Q2. Why are constant factors ignored?

**Answer:**
For sufficiently large input sizes, the growth rate dominates constant multipliers. Hence, $5000n^2$ is asymptotically better than $n^3$.

---

### Q3. Why is worst-case analysis commonly used?

**Answer:**
Because it provides a guaranteed upper bound on the running time and is easier to analyze than average-case complexity.

---

### Q4. Why are exponential algorithms considered impractical?

**Answer:**
Because their running time grows extremely rapidly. Even for $n=100$, an $O(2^n)$ algorithm becomes computationally infeasible.

---

# Flashcards

**Q:** What is Time Complexity?

**A:** The running time of an algorithm expressed as a function of input size.

---

**Q:** What is Space Complexity?

**A:** The amount of additional memory required during execution.

---

**Q:** What does asymptotic analysis study?

**A:** Algorithm performance as the input size approaches infinity.

---

**Q:** Which complexity is better: O(n²) or O(n log n)?

**A:** O(n log n).

---

**Q:** Why do we ignore constants?

**A:** Because asymptotic analysis focuses on growth rate rather than exact execution time.

---

# Practice MCQs

### Q1. Which complexity grows the slowest?

A. O(n²)

B. O(n log n)

C. O(log n)

D. O(2ⁿ)

**Answer:** C

---

### Q2. Which complexity is considered practical for very large datasets?

A. O(n!)

B. O(2ⁿ)

C. O(n log n)

D. O(n³)

**Answer:** C

---

### Q3. Which case is most commonly analyzed in algorithm design?

A. Best Case

B. Average Case

C. Worst Case

D. Random Case

**Answer:** C

---

### Q4. Why is algorithm analysis hardware-independent?

A. Hardware never changes.

B. We measure growth in terms of basic operations instead of execution time.

C. CPUs execute every instruction in exactly one cycle.

D. Programming languages always run at the same speed.

**Answer:** B

---

# One-Page Revision

* Time Complexity → Running time.
* Space Complexity → Memory usage.
* Running time represented by **T(n)**.
* Analyze algorithms as **n → ∞**.
* Ignore constants.
* Binary Search → **O(log n)**.
* Efficient Sorting → **O(n log n)**.
* Nested Loops → **O(n²)**.
* Worst Case → Standard method of analysis.
* Better algorithms outperform better hardware.