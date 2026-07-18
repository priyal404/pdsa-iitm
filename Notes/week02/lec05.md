# Lecture 5: Selection Sort

> **Course:** Programming, Data Structures and Algorithms
>
> **Week:** 2
>
> **Lecture:** 5

---

# Introduction

Binary Search demonstrated how sorting a list enables much faster searching.

However, before Binary Search can be applied, the data must first be sorted.

Sorting is one of the most fundamental problems in computer science because many other computational tasks become simpler and more efficient once the data is arranged in order.

This lecture introduces **Selection Sort**, one of the simplest sorting algorithms. Although it is not the most efficient algorithm, it provides an excellent introduction to algorithm design and complexity analysis.

---

# Why Do We Sort?

Sorting is useful for much more than searching.

Once a list is sorted, several operations become easier.

Some common applications include:

- Performing Binary Search efficiently.
- Finding the median of a dataset.
- Detecting duplicate values.
- Building frequency tables.
- Ranking or ordering records.

Sorting is therefore often used as a preprocessing step before solving more complex problems.

---

# Example: Finding the Median

The **median** is the value that divides a dataset into two equal halves.

If the list is unsorted,

```text
[42, 17, 95, 28, 60]
```

finding the median is not straightforward.

After sorting,

```text
[17, 28, 42, 60, 95]
```

the median is simply the middle element.

No additional computation is required.

---

# Example: Detecting Duplicates

Suppose we wish to determine whether a list contains repeated values.

Without sorting,

each value may have to be compared with many others.

After sorting,

```text
[15, 22, 22, 31, 45, 45, 60]
```

equal values automatically appear next to one another.

The problem is reduced to comparing only adjacent elements.

---

# Example: Building Frequency Tables

When equal values are grouped together,

counting occurrences becomes much easier.

For example,

```text
12 12 12 18 18 24 31 31
```

immediately reveals the frequency of each value.

Instead of searching throughout the list,

we simply count consecutive identical elements.

---

# The Selection Sort Idea

Selection Sort repeatedly selects the smallest remaining element and places it into its correct position.

After every iteration,

one more element reaches its final sorted position.

The unsorted portion of the list gradually becomes smaller until the entire list is sorted.

---

# A Real-Life Analogy

Imagine arranging a stack of examination papers in increasing order of marks.

A natural strategy is:

1. Find the paper with the lowest mark.
2. Place it at the beginning.
3. Ignore it from now on.
4. Repeat the process with the remaining papers.

Selection Sort follows exactly this approach.

---

# Example

Consider the list

```text
[64, 74, 32, 89, 21, 55]
```

---

## First Pass

The smallest value is

```text
21
```

Move it to the beginning.

```text
[21, 74, 32, 89, 64, 55]
```

---

## Second Pass

Ignore the first element.

Search only the remaining portion.

The smallest remaining value is

```text
32
```

Swap it into the second position.

```text
[21, 32, 74, 89, 64, 55]
```

---

## Third Pass

Ignore the first two elements.

The smallest remaining value is

```text
55
```

After swapping,

```text
[21, 32, 55, 89, 64, 74]
```

---

## Continue

Repeating the same process eventually produces

```text
[21, 32, 55, 64, 74, 89]
```

After every iteration,

one additional element reaches its final position.

---

# In-Place Selection Sort

Instead of creating a second list,

Selection Sort can rearrange the elements within the original list.

Whenever the minimum element is found,

it is swapped with the first element of the unsorted region.

This makes Selection Sort an **in-place sorting algorithm**, requiring only a small amount of additional memory.

---

# High-Level Algorithm

For each position in the list,

1. Assume the current position contains the smallest element.
2. Search the remaining part of the list.
3. Find the actual smallest element.
4. Swap it with the current position.

Then move to the next position and repeat.

---

# Pseudo-code

```text
for i = 0 to n-1

    minimum = i

    for j = i+1 to n-1

        if L[j] < L[minimum]:
            minimum = j

    swap L[i] and L[minimum]
```

The outer loop determines where the next smallest element should be placed.

The inner loop searches for that smallest element.

# Loop Invariant

When designing an algorithm, it is important not only to know *how* it works, but also *why* it works.

A common technique for proving the correctness of iterative algorithms is the **loop invariant**.

A loop invariant is a property that remains true every time the loop begins a new iteration.

For Selection Sort, the invariant is:

> **Before the start of iteration \(i\), the subarray \(L[0 \ldots i-1]\) is already sorted and contains the smallest \(i\) elements of the original list.**

Initially,

- no elements have been processed,
- so the invariant holds trivially.

During each iteration,

- the smallest element in the unsorted portion is found,
- and moved to position \(i\).

As a result,

the sorted portion grows by one element.

After the swap,

the invariant becomes

> **\(L[0 \ldots i]\) is sorted.**

Eventually,

when every position has been processed,

the entire list is sorted.

---

# Why the Algorithm Is Correct

Correctness must always be established before analyzing efficiency.

An algorithm that produces incorrect results is useless regardless of how fast it runs.

Selection Sort is correct because:

- Initially, the sorted portion is empty.
- Each iteration places the correct minimum element into its final position.
- The loop invariant remains true after every iteration.
- When the algorithm terminates, every element has been placed in its correct position.

Therefore, the final list is completely sorted.

---

# Complexity Analysis

Selection Sort contains two nested loops.

The outer loop chooses the position where the next smallest element will be placed.

```text
for i = 0 to n-1
```

This executes approximately

$$
n
$$

times.

---

For every value of

$$
i,
$$

the inner loop scans the remaining unsorted portion of the list.

Initially, it examines

$$
n-1
$$

elements.

During the next iteration,

it examines

$$
n-2
$$

elements.

The process continues until only one element remains.

The total number of comparisons is therefore

$$
(n-1)+(n-2)+\cdots+2+1.
$$

---

# Summation Formula

The above summation is

$$
1+2+\cdots+(n-1).
$$

Using the well-known formula,

$$
1+2+\cdots+n
=
\frac{n(n+1)}{2},
$$

we obtain

$$
\frac{n(n-1)}{2}.
$$

Expanding,

$$
\frac{n(n-1)}{2}
=
\frac{n^2}{2}-\frac{n}{2}.
$$

Ignoring lower-order terms and constant factors,

$$
T(n)=O(n^2).
$$

---

# Gauss's Trick

The summation

$$
1+2+\cdots+n
$$

can also be derived using a simple observation.

Write the sum forwards:

$$
1+2+3+\cdots+n
$$

and backwards:

$$
n+(n-1)+(n-2)+\cdots+1.
$$

Adding both expressions term by term,

every column equals

$$
n+1.
$$

Since there are

$$
n
$$

columns,

the total becomes

$$
n(n+1).
$$

Because the sum has been counted twice,

$$
1+2+\cdots+n
=
\frac{n(n+1)}{2}.
$$

This technique is commonly known as **Gauss's summation trick**.

---

# Best Case vs Worst Case

An interesting property of Selection Sort is that its running time is almost independent of the input order.

Whether the list is

- already sorted,
- completely random,
- or sorted in reverse order,

the algorithm still searches the entire unsorted portion during every iteration.

For example,

```text
[1, 2, 3, 4, 5]
```

and

```text
[5, 4, 3, 2, 1]
```

both require essentially the same number of comparisons.

Therefore,

- Best case: \(O(n^2)\)
- Average case: \(O(n^2)\)
- Worst case: \(O(n^2)\)

Unlike some sorting algorithms, Selection Sort gains almost no advantage from an already sorted list.

---

# Characteristics of Selection Sort

### Advantages

- Simple to understand and implement.
- Works in-place without requiring an additional array.
- Performs relatively few swaps.

### Disadvantages

- Requires a quadratic number of comparisons.
- Does not adapt to partially sorted input.
- Becomes inefficient for large datasets.

---

# Key Takeaways

- Selection Sort repeatedly selects the smallest remaining element.
- The algorithm maintains a growing sorted prefix.
- A loop invariant provides a formal proof of correctness.
- Two nested loops lead to quadratic running time.
- Selection Sort performs

$$
\frac{n(n-1)}{2}
$$

comparisons.

- Time complexity is

$$
O(n^2)
$$

in the best, average, and worst cases.

---

# GATE / Interview Focus

- Selection Sort is an **in-place comparison sorting algorithm**.
- It repeatedly selects the minimum element from the unsorted portion.
- The sorted portion grows by one element after each iteration.
- Loop invariant:

> Before iteration \(i\), the first \(i\) elements are already sorted.

- Time complexity:

$$
O(n^2)
$$

for all cases.

- Space complexity:

$$
O(1).
$$

---

# Flashcards

**Q:** What is the basic idea of Selection Sort?

**A:** Repeatedly find the smallest remaining element and place it in its correct position.

---

**Q:** What is the loop invariant of Selection Sort?

**A:** Before iteration \(i\), the first \(i\) elements are already sorted.

---

**Q:** What is the worst-case time complexity of Selection Sort?

**A:** \(O(n^2)\).

---

**Q:** Does Selection Sort require extra memory?

**A:** No, it is an in-place sorting algorithm with \(O(1)\) auxiliary space.

---

**Q:** Does Selection Sort become faster for an already sorted list?

**A:** No. It performs essentially the same number of comparisons regardless of input order.

---

# Practice MCQs

### Q1

Selection Sort repeatedly selects the

A. Largest element

B. Smallest remaining element

C. Middle element

D. Random element

**Answer:** B

---

### Q2

Selection Sort requires

A. \(O(1)\)

B. \(O(\log n)\)

C. \(O(n)\)

D. \(O(n^2)\)

comparisons in the worst case.

**Answer:** D

---

### Q3

Selection Sort is

A. Recursive

B. Divide-and-conquer

C. In-place

D. Hash-based

**Answer:** C

---

### Q4

The auxiliary space complexity of Selection Sort is

A. \(O(n)\)

B. \(O(\log n)\)

C. \(O(1)\)

D. \(O(n^2)\)

**Answer:** C

---

### Q5

Selection Sort performs significantly better on an already sorted list.

A. True

B. False

**Answer:** B

---

# One-Page Revision

- Selection Sort repeatedly places the smallest remaining element into its correct position.
- Maintains a sorted prefix and an unsorted suffix.
- Proven correct using a **loop invariant**.
- Number of comparisons:

$$
\frac{n(n-1)}{2}.
$$

- Time complexity:

$$
O(n^2)
$$

in all cases.

- Auxiliary space:

$$
O(1).
$$

- Simple algorithm, but inefficient for large inputs due to quadratic running time.