# Lecture 3: Calculating Complexity

> **Course:** Programming, Data Structures and Algorithms
>
> **Week:** 2
>
> **Lecture:** 3

---

# Introduction

In the previous lectures, we introduced **asymptotic analysis** and the use of **Big O notation** to compare algorithms. The next step is to determine the complexity of actual programs.

In practice, algorithms are usually implemented in one of two ways:

1. **Iterative algorithms**, which use loops.
2. **Recursive algorithms**, where a function repeatedly calls itself.

The goal of this lecture is to understand how to estimate the running time of both types of algorithms by analyzing their structure rather than measuring execution time experimentally.

---

# Complexity of Iterative Programs

For iterative programs, the running time is determined primarily by the number of times each loop executes.

A program without any loops performs only a fixed number of operations and therefore has **constant time complexity**, $O(1)$.

As loops are introduced, the running time begins to depend on the input size.

General guidelines are:

- A single loop usually contributes a linear factor.
- Nested loops multiply their contributions.
- Sequential loops contribute additively, after which the dominant term is retained.

Therefore, calculating the complexity of an iterative algorithm often reduces to counting loop iterations.

---

# Example 1: Finding the Maximum Element

Consider the problem of finding the largest element in an unsorted list.

The algorithm proceeds as follows:

1. Assume that the first element is the maximum.
2. Scan the remaining elements one by one.
3. Whenever a larger element is found, update the current maximum.
4. After reaching the end of the list, return the maximum value.

Pseudo-code:

```text
max = L[0]

for each element x in L:
    if x > max:
        max = x

return max
```

---

# Determining the Input Size

Before analyzing any algorithm, we must first identify its **input size**.

For list-processing algorithms, the natural choice is:

$$
n = \text{length of the list}
$$

A larger list requires more comparisons, making the running time directly dependent on $n$.

---

# Complexity Analysis

The algorithm performs a **single scan** of the list.

Regardless of where the maximum element is located,

- at the beginning,
- in the middle,
- or at the end,

every element must still be examined.

Therefore, the loop always executes exactly $n$ times.

Hence,

$$
T(n)=O(n).
$$

---

# Observation

Unlike some search algorithms, this algorithm does **not** terminate early.

Even if the first element is the largest, the algorithm has no way of knowing this without checking every remaining element.

As a result,

- Best case = $O(n)$
- Worst case = $O(n)$
- Average case = $O(n)$

This is an example where all cases have the same asymptotic complexity.

---

# Example 2: Detecting Duplicate Elements

Suppose we are given an unsorted list and wish to determine whether every element is distinct.

A straightforward approach is to compare every element with every element that appears after it.

Pseudo-code:

```text
for i = 0 to n-1
    for j = i+1 to n-1
        if L[i] == L[j]:
            return False

return True
```

---

# Why Compare Only Elements to the Right?

Notice that the inner loop begins from

$$
j=i+1.
$$

This avoids unnecessary comparisons.

For example,

if we compare

$$
L[2]
$$

with

$$
L[5],
$$

there is no need to compare

$$
L[5]
$$

with

$$
L[2]
$$

again.

Similarly,

an element never needs to be compared with itself.

This reduces redundant work while still checking every distinct pair exactly once.

---

# Counting Comparisons

The outer loop executes approximately

$$
n
$$

times.

The inner loop executes:

- $n-1$ times during the first iteration,
- $n-2$ times during the second,
- ...
- $1$ time during the final useful iteration.

Therefore, the total number of comparisons is

$$
(n-1)+(n-2)+\cdots+2+1.
$$

Using the well-known formula,

$$
1+2+\cdots+(n-1)
=
\frac{n(n-1)}{2}.
$$

---

# Simplifying the Expression

Expanding,

$$
\frac{n(n-1)}{2}
=
\frac{n^2}{2}-\frac{n}{2}.
$$

Ignoring the constant factor and the lower-order term,

we obtain

$$
T(n)=O(n^2).
$$

Thus, the duplicate detection algorithm has **quadratic time complexity**.

---

# Best Case vs Worst Case

Unlike the previous example, this algorithm may terminate early.

### Best Case

Suppose

$$
L[0]=L[1].
$$

The algorithm detects a duplicate immediately and returns after only one comparison.

Running time:

$$
O(1).
$$

---

### Worst Case

If every element in the list is distinct,

the algorithm must compare **every possible pair** before concluding that no duplicates exist.

This requires

$$
\frac{n(n-1)}{2}
$$

comparisons.

Therefore,

the worst-case complexity is

$$
O(n^2).
$$

---

# Important Observation

Worst-case analysis assumes that the algorithm performs the maximum possible amount of work.

For this problem,

the worst case occurs **not when duplicates exist**, but when **no duplicates exist at all**.

Only after examining every possible pair can the algorithm confidently return `True`.

---

# Matrix Multiplication

A more computationally intensive example is **matrix multiplication**.

Suppose we have two compatible matrices:

- Matrix $A$ of size $m \times n$
- Matrix $B$ of size $n \times p$

Their product is a matrix

$$
C=A\times B
$$

having dimensions

$$
m\times p.
$$

Each element of the output matrix is computed by multiplying one row of the first matrix with one column of the second matrix.

---

# Computing One Element

The element

$$
C_{ij}
$$

is obtained by

$$
C_{ij}
=
\sum_{k=0}^{n-1}
A_{ik}B_{kj}.
$$

Thus,

each output element requires

$$
n
$$

multiplications and additions.

---

# Algorithm Structure

The standard matrix multiplication algorithm contains three nested loops.

```text
for i = 0 to m-1
    for j = 0 to p-1
        for k = 0 to n-1
            C[i][j] += A[i][k] * B[k][j]
```

---

# Complexity Analysis

The loops execute:

- Outer loop: $m$ iterations
- Middle loop: $p$ iterations
- Inner loop: $n$ iterations

Hence,

$$
T(m,n,p)=O(mnp).
$$

---

# Square Matrices

If all matrices are square,

$$
m=n=p,
$$

then

$$
T(n)=O(n^3).
$$

This is one of the first examples of an algorithm whose complexity is cubic rather than quadratic.

---

# Logarithmic Complexity

Not every algorithm processes the entire input one element at a time.

Some algorithms repeatedly reduce the problem size, often by dividing it into smaller parts. These algorithms usually exhibit **logarithmic time complexity**.

Consider the problem of determining the number of bits required to represent a positive integer in binary.

One simple approach is:

1. Divide the number by 2 repeatedly.
2. Count how many divisions are performed before the value becomes 1.

Pseudo-code:

```text
count = 1

while n > 1:
    n = n // 2
    count += 1

return count
```

---

# Complexity Analysis

Each iteration halves the current value of $n$.

The sequence of values becomes

$$
n,\;
\frac{n}{2},\;
\frac{n}{4},\;
\frac{n}{8},
\ldots,
1.
$$

Suppose the loop executes $k$ times.

After $k$ divisions,

$$
\frac{n}{2^k}=1.
$$

Therefore,

$$
2^k=n,
$$

which implies

$$
k=\log_2 n.
$$

Hence,

$$
T(n)=O(\log n).
$$

---

# An Important Observation About Input Size

For number-theoretic algorithms, the value of the number itself is **not** the appropriate measure of input size.

Instead, the input size should be the number of digits required to represent the number.

For an integer,

- Binary representation requires approximately $\log_2 n$ bits.
- Decimal representation requires approximately $\log_{10} n$ digits.

Since logarithms with different bases differ only by a constant factor,

$$
\log_a n=\frac{\log_b n}{\log_b a},
$$

they belong to the same asymptotic order.

Thus,

$$
O(\log_2 n)=O(\log_{10} n)=O(\log n).
$$

This means that the algorithm above is actually **linear in the size of its input**, even though its running time is expressed as $O(\log n)$ with respect to the numeric value.

---

# Recursive Algorithms

Unlike iterative algorithms, recursive algorithms solve a problem by repeatedly reducing it to smaller instances of the same problem.

To analyze their complexity, we usually express the running time using a **recurrence relation**.

A recurrence defines the complexity of a problem in terms of the complexity of smaller subproblems.

Once the recurrence is established, it can be solved to obtain the overall time complexity.

---

# Example: Tower of Hanoi

The Tower of Hanoi is a classic recursive problem.

We are given:

- Three pegs.
- $n$ discs of different sizes.
- Initially, all discs are stacked on one peg in decreasing order of size.

The objective is to move the entire stack to another peg while following two rules:

1. Only one disc may be moved at a time.
2. A larger disc can never be placed on top of a smaller disc.

---

# Recursive Strategy

Suppose there are $n$ discs.

The largest disc is at the bottom of the stack.

To move it,

1. Move the top $n-1$ discs to the auxiliary peg.
2. Move the largest disc to the destination peg.
3. Move the $n-1$ discs from the auxiliary peg onto the largest disc.

Notice that the same problem of moving $n-1$ discs appears twice.

This naturally leads to recursion.

---

# Formulating the Recurrence

Let

$$
M(n)
$$

represent the minimum number of moves required to transfer $n$ discs.

The simplest case is

$$
M(1)=1.
$$

For larger values of $n$,

the recursive strategy requires:

- moving $n-1$ discs,
- moving one disc,
- moving $n-1$ discs again.

Therefore,

$$
M(n)=2M(n-1)+1.
$$

---

# Expanding the Recurrence

Substituting repeatedly,

$$
M(n)
=
2\left(2M(n-2)+1\right)+1.
$$

Simplifying,

$$
M(n)
=
2^2M(n-2)+2+1.
$$

Expanding once more,

$$
M(n)
=
2^3M(n-3)+4+2+1.
$$

A clear pattern begins to emerge.

After $k$ substitutions,

$$
M(n)
=
2^kM(n-k)
+
(2^k-1).
$$

---

# Reaching the Base Case

The expansion stops when

$$
n-k=1,
$$

which means

$$
k=n-1.
$$

Substituting,

$$
M(n)
=
2^{\,n-1}M(1)
+
2^{\,n-1}-1.
$$

Since

$$
M(1)=1,
$$

we obtain

$$
M(n)
=
2^n-1.
$$

Therefore,

$$
T(n)=O(2^n).
$$

---

# Interpretation

The running time doubles whenever one additional disc is added.

For example,

| Number of Discs | Minimum Moves |
|----------------:|--------------:|
| 1 | 1 |
| 2 | 3 |
| 3 | 7 |
| 4 | 15 |
| 5 | 31 |
| 10 | 1023 |
| 20 | 1,048,575 |

This rapid growth makes exponential algorithms impractical even for moderately large inputs.

---

# Comparing the Examples

| Problem | Complexity |
|---------|------------|
| Find maximum element | $O(n)$ |
| Detect duplicates | $O(n^2)$ |
| Matrix multiplication | $O(mnp)$ |
| Square matrix multiplication | $O(n^3)$ |
| Counting binary digits | $O(\log n)$ |
| Tower of Hanoi | $O(2^n)$ |

These examples illustrate how different algorithmic strategies lead to very different growth rates.

---

# General Strategy for Calculating Complexity

When analyzing an algorithm, the following steps are useful:

1. Identify the input size.
2. Determine whether the algorithm is iterative or recursive.
3. Count the number of loop iterations for iterative algorithms.
4. Formulate a recurrence for recursive algorithms.
5. Simplify the resulting expression using asymptotic notation.

Following these steps helps estimate the running time without executing the program.

---

# Common Mistakes

### 1. Choosing the Wrong Input Size

For list-processing algorithms, use the length of the list.

For numeric algorithms, use the number of digits required to represent the number rather than its value.

---

### 2. Counting Statements Instead of Loops

Most simple statements execute in constant time.

The dominant contribution usually comes from loops or recursive calls.

---

### 3. Confusing Nested and Sequential Loops

Sequential loops add their complexities.

Nested loops multiply them.

---

### 4. Ignoring the Base Case in Recursive Analysis

Every recurrence must include a valid stopping condition.

Without a base case, the recurrence cannot be solved correctly.

---

# Key Takeaways

- Complexity analysis estimates how an algorithm scales with increasing input size.
- Iterative algorithms are analyzed by counting loop iterations.
- Recursive algorithms are analyzed using recurrence relations.
- Logarithmic algorithms repeatedly reduce the problem size.
- Exponential algorithms grow extremely quickly and become impractical for large inputs.
- Selecting the correct measure of input size is essential for accurate complexity analysis.

---

# GATE / Interview Focus

- Always identify the input size before analyzing complexity.
- A single loop usually contributes $O(n)$.
- Nested loops multiply their complexities.
- Repeated halving leads to logarithmic complexity.
- Recursive algorithms are analyzed using recurrences.
- The recurrence for Tower of Hanoi is

$$
M(n)=2M(n-1)+1,
$$

whose solution is

$$
M(n)=2^n-1.
$$

- Exponential algorithms become infeasible as the input size increases.

---

# Flashcards

**Q:** What determines the complexity of an iterative algorithm?

**A:** The number of loop iterations.

---

**Q:** How are recursive algorithms usually analyzed?

**A:** By writing and solving a recurrence relation.

---

**Q:** Why does repeated halving produce logarithmic complexity?

**A:** Because the number of halvings needed to reach 1 is $\log n$.

---

**Q:** What recurrence describes the Tower of Hanoi?

**A:**

$$
M(n)=2M(n-1)+1.
$$

---

**Q:** What is the complexity of the Tower of Hanoi algorithm?

**A:** $O(2^n)$.

---

# Practice MCQs

### Q1

Finding the maximum element in an unsorted list requires

A. $O(1)$

B. $O(\log n)$

C. $O(n)$

D. $O(n^2)$

**Answer:** C

---

### Q2

The naive duplicate detection algorithm has worst-case complexity

A. $O(n)$

B. $O(n\log n)$

C. $O(n^2)$

D. $O(2^n)$

**Answer:** C

---

### Q3

The standard algorithm for multiplying two square matrices has complexity

A. $O(n^2)$

B. $O(n^3)$

C. $O(n\log n)$

D. $O(2^n)$

**Answer:** B

---

### Q4

Repeatedly dividing a number by 2 until it becomes 1 requires

A. $O(1)$

B. $O(\log n)$

C. $O(n)$

D. $O(n^2)$

**Answer:** B

---

### Q5

The Tower of Hanoi algorithm has

A. Linear complexity

B. Quadratic complexity

C. Cubic complexity

D. Exponential complexity

**Answer:** D

---

# One-Page Revision

- Complexity depends on how the amount of work grows with input size.
- Count loop iterations for iterative algorithms.
- Write recurrences for recursive algorithms.
- Single loop → $O(n)$.
- Nested loops → Multiply complexities.
- Repeated halving → $O(\log n)$.
- Standard square matrix multiplication → $O(n^3)$.
- Tower of Hanoi recurrence:

$$
M(n)=2M(n-1)+1.
$$

- Tower of Hanoi complexity:

$$
O(2^n).
$$

- Exponential algorithms become impractical for large inputs.