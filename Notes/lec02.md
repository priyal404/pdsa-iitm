# Lecture 2: Comparing Orders of Magnitude

> **Course:** Programming, Data Structures and Algorithms
>
> **Week:** 2
>
> **Lecture:** 2

---

# Introduction

In the previous lecture, we learned how to measure the efficiency of an algorithm using **time complexity**. However, knowing the running time alone is not sufficient. We also need a way to compare different algorithms and determine which one scales better as the input size increases.

Consider two algorithms with running times:

- $5000n^2$
- $n^3$

For small values of $n$, the second algorithm may appear faster. However, as $n$ grows larger, the cubic function eventually overtakes the quadratic one. This observation motivates the need to compare **growth rates** instead of exact execution times.

Asymptotic analysis provides a mathematical framework for making these comparisons.

---

# Comparing Growth Rates

Suppose two algorithms have running times:

- $f(n)$
- $g(n)$

Rather than comparing their exact values for every input, we ask a simpler question:

> **Which function grows faster when the input becomes very large?**

This comparison helps us determine which algorithm remains efficient as the problem size increases.

---

# Orders of Magnitude

The **order of magnitude** of a function describes how quickly it grows with increasing input size.

Algorithms having the same order of magnitude exhibit similar long-term behaviour, even if their exact running times differ because of constants or lower-order terms.

For example,

- $100n$
- $5n$
- $n$

all belong to the same order of growth because they increase linearly.

Similarly,

- $n^2$
- $10n^2$
- $500n^2$

all have quadratic growth.

---

# Why Ignore Constants?

Suppose two algorithms require:

- $10n$
- $500n$

operations.

Although the second algorithm performs fifty times more work, both grow **linearly**.

As the input size increases, this constant factor remains fixed and does not affect the overall trend.

Therefore, asymptotic analysis ignores constant multipliers and focuses only on the dominant growth rate.

---

# Big O Notation

Big O notation provides an **upper bound** on the growth of a function.

If an algorithm has complexity

$O(g(n))$,

it means that its running time will never grow faster than a constant multiple of $g(n)$ for sufficiently large values of $n$.

Big O therefore describes the **worst-case growth rate** of an algorithm.

---

# Formal Definition

A function $f(n)$ is said to belong to $O(g(n))$ if there exist positive constants $c$ and $n_0$ such that

$$
f(n)\le cg(n)
$$

for every

$$
n\ge n_0.
$$

The definition introduces two important constants.

### Constant $c$

The comparison function may be multiplied by any positive constant.

This allows us to ignore implementation-specific factors such as processor speed or programming language.

### Threshold $n_0$

The inequality does not have to hold for small values of $n$.

Only the behaviour beyond some sufficiently large input size matters.

---

# Understanding the Definition Intuitively

Imagine plotting two curves on a graph.

- The first curve represents $f(n)$.
- The second curve represents $cg(n)$.

Initially, the curves may intersect several times.

However, once the input size reaches $n_0$, the graph of $cg(n)$ always stays above $f(n)$.

This indicates that $g(n)$ grows at least as quickly as $f(n)$ up to a constant factor.

---

# Example 1

Show that

$$
100n+5=O(n^2).
$$

## Step 1

Assume

$$
n\ge5.
$$

Since

$$
5\le n,
$$

we obtain

$$
100n+5\le100n+n.
$$

---

## Step 2

Combine the terms.

$$
100n+n=101n.
$$

---

## Step 3

Because

$$
n\ge1,
$$

we know

$$
101n\le101n^2.
$$

Hence,

$$
100n+5\le101n^2.
$$

Choosing

- $c=101$
- $n_0=5$

satisfies the definition of Big O.

Therefore,

$$
100n+5=O(n^2).
$$

---

# Important Observation

The constants chosen during a Big O proof are **not unique**.

For the previous example, another valid proof is obtained by observing that

$$
5\le5n
$$

for all

$$
n\ge1.
$$

This gives

$$
100n+5\le100n+5n=105n.
$$

Since

$$
105n\le105n^2,
$$

another valid choice is

- $c=105$
- $n_0=1$

Different constants lead to the same asymptotic conclusion.

---

# Example 2

Determine the complexity of

$$
100n^2+20n+5.
$$

Since

$$
20n\le20n^2
$$

and

$$
5\le5n^2
$$

for

$$
n\ge1,
$$

we obtain

$$
100n^2+20n+5
\le100n^2+20n^2+5n^2
=125n^2.
$$

Therefore,

$$
100n^2+20n+5=O(n^2).
$$

---

# Dominant Term Principle

For polynomial functions, the term with the highest power of $n$ eventually dominates all others.

Examples:

| Function | Big O |
|----------|--------|
| $5n^2+3n+1$ | $O(n^2)$ |
| $8n^3+100n^2+50$ | $O(n^3)$ |
| $12n^4+n^2+100$ | $O(n^4)$ |

The lower-order terms become insignificant as the input size increases.

---

# Comparing Common Growth Rates

Some frequently encountered growth rates are shown below in increasing order.

| Complexity | Description |
|------------|-------------|
| $O(1)$ | Constant |
| $O(\log n)$ | Logarithmic |
| $O(\sqrt n)$ | Square Root |
| $O(n)$ | Linear |
| $O(n\log n)$ | Linearithmic |
| $O(n^2)$ | Quadratic |
| $O(n^3)$ | Cubic |
| $O(2^n)$ | Exponential |
| $O(n!)$ | Factorial |

A slower-growing function generally corresponds to a more efficient algorithm for large inputs.

---

# Comparing Different Functions

Some useful asymptotic relationships are:

- $\log n < \sqrt n$
- $\sqrt n < n$
- $n < n\log n$
- $n\log n < n^2$
- $n^2 < n^3$
- $n^k < 2^n$ for every fixed positive integer $k$
- $2^n < n!$ for sufficiently large $n$

Remember that these comparisons are valid **asymptotically**, not necessarily for very small values of $n$.

---

# Key Ideas So Far

- Big O describes an **upper bound** on the growth of a function.
- Constants and lower-order terms are ignored because they do not affect long-term behaviour.
- Only sufficiently large inputs are considered in asymptotic analysis.
- The highest-degree term determines the complexity of a polynomial.
- Comparing algorithms means comparing their rates of growth rather than exact execution times.

---

---

# Properties of Big O

Big O notation possesses several useful mathematical properties that make algorithm analysis much simpler. Rather than deriving the complexity from scratch every time, these properties allow us to combine and simplify complexity expressions systematically.

---

# Property 1: Constant Multiplication

Multiplying a function by a positive constant does not change its asymptotic complexity.

If

$$
f(n)=O(g(n)),
$$

then for any positive constant $k$,

$$
kf(n)=O(g(n)).
$$

### Example

The following functions all have the same asymptotic complexity:

- $n$
- $10n$
- $5000n$

Therefore,

$$
10n=O(n)
$$

and

$$
5000n=O(n).
$$

The difference is only a constant factor, which becomes insignificant for sufficiently large input sizes.

---

# Property 2: Addition Rule

Suppose an algorithm performs two independent operations whose running times are

- $f(n)$
- $g(n)$

The total running time becomes

$$
f(n)+g(n).
$$

The overall complexity is determined by the faster-growing function.

### Example

$$
n+n^2
$$

Since

$$
n^2
$$

grows much faster than

$$
n,
$$

we write

$$
O(n+n^2)=O(n^2).
$$

Similarly,

$$
n^3+200n^2+5n
$$

simplifies to

$$
O(n^3).
$$

### Rule

When adding complexities,

> **Keep only the dominant term.**

---

# Sequential Algorithms

Many algorithms execute one statement after another.

Consider the following pseudo-code.

```text
Step 1 : O(n)

Step 2 : O(n²)

Step 3 : O(log n)
```

The total complexity is

$$
O(n+n^2+\log n).
$$

Since $n^2$ dominates the remaining terms,

the overall complexity becomes

$$
O(n^2).
$$

---

# Nested Loops

Unlike sequential statements,

**nested loops multiply their complexities.**

Example:

```text
for i = 1 to n
    for j = 1 to n
        ...
```

Outer loop:

$$
O(n)
$$

Inner loop:

$$
O(n)
$$

Overall complexity:

$$
O(n)\times O(n)=O(n^2).
$$

---

### Triple Nested Loops

```text
for i = 1 to n
    for j = 1 to n
        for k = 1 to n
            ...
```

Complexity:

$$
O(n^3).
$$

---

# Sequential vs Nested Loops

This is one of the most common sources of confusion.

### Sequential

```text
for i = 1 to n
    ...

for j = 1 to n
    ...
```

Complexity:

$$
O(n+n)=O(n).
$$

---

### Nested

```text
for i = 1 to n
    for j = 1 to n
        ...
```

Complexity:

$$
O(n^2).
$$

Remember:

- Sequential → Addition
- Nested → Multiplication

---

# Big Omega ($\Omega$)

Big O provides an **upper bound**.

Sometimes we also need a **lower bound**, which tells us the minimum growth rate of a function.

This is represented using **Big Omega**.

---

# Definition

A function $f(n)$ belongs to $\Omega(g(n))$ if there exist positive constants $c$ and $n_0$ such that

$$
f(n)\ge cg(n)
$$

for every

$$
n\ge n_0.
$$

---

# Interpretation

Big Omega guarantees that

> the running time of an algorithm cannot grow **slower** than a constant multiple of $g(n)$.

It therefore represents a lower bound on the asymptotic growth.

---

# Example

Consider

$$
5n^2+20n+7.
$$

Clearly,

$$
5n^2+20n+7\ge5n^2.
$$

Hence,

$$
5n^2+20n+7=\Omega(n^2).
$$

---

# Big Theta ($\Theta$)

Big O provides an upper bound.

Big Omega provides a lower bound.

When **both** bounds are of the same order, we use **Big Theta**.

---

# Definition

A function $f(n)$ belongs to $\Theta(g(n))$ if there exist positive constants $c_1$, $c_2$, and $n_0$ such that

$$
c_1g(n)\le f(n)\le c_2g(n)
$$

for every

$$
n\ge n_0.
$$

---

# Interpretation

Big Theta represents the **exact asymptotic order** of a function.

It tells us that the function grows neither significantly faster nor significantly slower than $g(n)$.

---

# Example

Consider

$$
5n^2+20n+7.
$$

We have already shown

$$
5n^2+20n+7=O(n^2).
$$

Similarly,

$$
5n^2+20n+7=\Omega(n^2).
$$

Therefore,

$$
5n^2+20n+7=\Theta(n^2).
$$

---

# Relationship Between O, Ω and Θ

| Notation | Meaning |
|----------|---------|
| $O(g(n))$ | Upper Bound |
| $\Omega(g(n))$ | Lower Bound |
| $\Theta(g(n))$ | Tight Bound |

Think of them as:

- **Big O** → Maximum growth
- **Big Ω** → Minimum growth
- **Big Θ** → Actual asymptotic growth

---

# Common Mistakes

### 1. Keeping Constants

Incorrect:

$$
O(500n)
$$

Correct:

$$
O(n)
$$

---

### 2. Keeping Lower-Order Terms

Incorrect:

$$
O(n^2+n)
$$

Correct:

$$
O(n^2)
$$

---

### 3. Adding Nested Loop Complexities

Nested loops multiply.

Sequential loops add.

---

### 4. Confusing Big O with Exact Running Time

Big O does **not** represent the exact number of operations.

It only describes the growth trend for sufficiently large input sizes.

---

# Key Takeaways

- Big O provides an upper bound.
- Big Omega provides a lower bound.
- Big Theta provides a tight bound.
- Ignore constants and lower-order terms.
- Sequential statements add complexities.
- Nested loops multiply complexities.
- The highest-degree term determines the complexity of a polynomial.

---

# GATE / Interview Focus

### Remember

- Big O → Upper Bound
- Big Ω → Lower Bound
- Big Θ → Tight Bound
- Ignore constants.
- Ignore lower-order terms.
- Sequential loops → Addition.
- Nested loops → Multiplication.
- Highest-degree polynomial dominates.

### Frequently Asked Questions

**Q. Why is $8n^3+100n^2+50$ written as $O(n^3)$?**

Because the cubic term grows much faster than the quadratic and constant terms for sufficiently large values of $n$.

---

**Q. What is the difference between Big O and Big Theta?**

Big O provides only an upper bound, whereas Big Theta provides both upper and lower bounds, making it the exact asymptotic characterization.

---

**Q. Which notation represents the minimum asymptotic growth?**

Big Omega.

---

# Flashcards

**Q:** What does Big O represent?

**A:** An asymptotic upper bound.

---

**Q:** What does Big Omega represent?

**A:** An asymptotic lower bound.

---

**Q:** What does Big Theta represent?

**A:** A tight asymptotic bound.

---

**Q:** Which term determines the complexity of a polynomial?

**A:** The highest-degree term.

---

**Q:** How are sequential loop complexities combined?

**A:** By addition.

---

**Q:** How are nested loop complexities combined?

**A:** By multiplication.

---

# Practice MCQs

### Q1

The complexity of $8n^3+100n^2+50$ is

A. $O(n)$

B. $O(n^2)$

C. $O(n^3)$

D. $O(2^n)$

**Answer:** C

---

### Q2

Which notation represents a lower bound?

A. Big O

B. Big Ω

C. Big Θ

D. None

**Answer:** B

---

### Q3

Two sequential loops each execute $n$ times.

The total complexity is

A. $O(n)$

B. $O(n^2)$

C. $O(2n)$

D. $O(\log n)$

**Answer:** A

---

### Q4

Two nested loops each execute $n$ times.

The complexity is

A. $O(n)$

B. $O(n\log n)$

C. $O(n^2)$

D. $O(2n)$

**Answer:** C

---

### Q5

Which notation gives the exact asymptotic growth?

A. Big O

B. Big Ω

C. Big Θ

D. None

**Answer:** C

---

# One-Page Revision

- Compare algorithms using their **growth rates**, not exact running times.
- Big O gives an **upper bound**.
- Big Ω gives a **lower bound**.
- Big Θ gives a **tight (exact) asymptotic bound**.
- Ignore constants and lower-order terms.
- Highest-degree polynomial term dominates.
- Sequential statements → Add complexities.
- Nested loops → Multiply complexities.

### Common Growth Order

$$
O(1)
<
O(\log n)
<
O(\sqrt n)
<
O(n)
<
O(n\log n)
<
O(n^2)
<
O(n^3)
<
O(2^n)
<
O(n!)
$$

Algorithms with slower-growing complexities generally scale better and are preferred for large inputs.