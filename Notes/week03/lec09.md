# Lecture 09: Difference Between Lists and Arrays (Implementation)

> **Course:** Programming, Data Structures and Algorithms using Python
>
> **Week:** 3
>
> **Lecture:** 9

---

# Lecture Notes

## Overview

In the previous lectures, we learned the theoretical differences between **linked lists**, **arrays**, and **Python lists**.

This lecture validates those concepts through **experimental analysis**.

Instead of relying only on time complexity analysis, the professor measures the execution time of common operations such as:

- Appending to a Python list
- Inserting at the beginning of a list
- Searching
- Sorting

The experiments demonstrate that Python lists behave exactly like **dynamic arrays**, and also compare their performance with **NumPy arrays**.

---

## Experimental Setup

To perform timing experiments, Python's recursion limit is increased.

```python
import sys

sys.setrecursionlimit(2**31 - 1)
```

This allows recursive algorithms like Merge Sort and Quick Sort to execute without exceeding Python's default recursion depth.

A custom timer class is also used to accurately measure execution times.

---

## Experiment 1: Testing append()

We create an empty list and repeatedly append elements.

```python
L = []

for i in range(10**7):
    L.append(i)
```

This performs **10 million append operations**.

The experiment completes in approximately **1–2 seconds**, showing that appending remains very efficient even for extremely large lists.

---

## Why Is append() So Fast?

Python lists maintain extra unused space after the last element.

```
Allocated Array

+----+----+----+----+----+----+

10   20   30        Free Space

             ↑

      Next insertion point
```

Each call to

```python
append()
```

simply places the new element into the next available position.

Since no existing elements are shifted,

the operation takes constant time in most cases.

```
append()

Time Complexity = O(1) (Amortized)
```

Occasionally,

Python allocates a larger array and copies the existing elements,

but this happens infrequently enough that the average cost remains constant.

---

## Experiment 2: Testing insert()

Instead of appending,

elements are inserted at the beginning of the list.

```python
L = []

for i in range(100000):
    L.insert(0, i)
```

Unlike append,

every insertion requires all existing elements to shift one position to the right.

Example:

Before

```
10 20 30
```

Insert

```
5
```

After

```
5 10 20 30
```

Each insertion becomes increasingly expensive as the list grows.

---

## Experimental Results

The professor performs the following experiments:

| Number of Inserts | Approximate Time |
|------------------:|-----------------:|
| 100,000 | ~2 seconds |
| 200,000 | ~10 seconds |
| 300,000 | ~22 seconds |

Notice that

doubling the input size increases the running time by roughly **four times**,

while tripling the input increases the running time by roughly **nine times**.

This is characteristic of **quadratic growth**.

---

## Why Does insert() Behave Like O(n²)?

Suppose we repeatedly insert at the beginning.

The first insertion shifts

```
0
```

elements.

The second shifts

```
1
```

element.

The third shifts

```
2
```

elements.

Continuing,

the total work becomes

```
0 + 1 + 2 + ... + (n−1)
```

which equals

```
n(n−1)/2
```

Therefore,

the total running time grows proportionally to

```
O(n²)
```

This experimentally confirms that Python lists are **dynamic arrays**, not linked lists.

If Python lists were true linked lists,

inserting at the front would have required only constant time.

---

## Conclusion from the First Experiments

The timing experiments validate the implementation discussed in the previous lecture.

They show that:

- Appending is extremely efficient.
- Inserting at the beginning is expensive.
- The cost of insertion grows quadratically when repeated many times.

These results strongly support the conclusion that **Python lists are implemented as dynamic arrays** rather than linked lists.

---

---

# Key Takeaways

- Python lists are implemented as dynamic arrays, making `append()` efficient but insertions at the beginning expensive.
- Experimental results confirm that `append()` runs in amortized **O(1)** time, while repeated insertion at the front exhibits **O(n²)** behavior.
- Doubling the input size for repeated front insertions approximately quadruples the execution time, validating quadratic complexity.
- Searching algorithms perform differently depending on both the algorithm and the underlying data structure.
- Binary search remains significantly faster than linear search due to its logarithmic complexity.
- Although NumPy arrays represent true arrays, they are not always faster than Python lists for searching and sorting operations.
- Selection sort performs similarly regardless of input order but is generally slower on NumPy arrays than on Python lists.
- Merge sort maintains its **O(n log n)** complexity on both data structures but incurs additional overhead when using NumPy arrays.
- Choosing the correct data structure depends on the intended application rather than theoretical complexity alone.
- Python lists are generally preferred for ordinary sequence manipulation, while NumPy arrays are best suited for numerical and matrix computations.

---

# Summary

This lecture experimentally verifies the theoretical differences between Python lists and NumPy arrays. Python lists, although called "lists," are internally implemented as dynamic arrays. The experiments demonstrate that appending elements is highly efficient due to amortized constant-time resizing, whereas repeatedly inserting elements at the beginning results in quadratic running time because existing elements must be shifted. The lecture also compares searching and sorting algorithms on Python lists and NumPy arrays. While binary search remains significantly faster than linear search, NumPy arrays do not consistently outperform Python lists for indexing-based algorithms such as searching and sorting. The results emphasize that selecting the appropriate data structure depends on the nature of the operations being performed: Python lists are ideal for general-purpose programming, whereas NumPy arrays excel in numerical and matrix-oriented computations.

---

# Flashcards

### Flashcard 1

**Q:** What experiment verifies that Python lists are implemented as dynamic arrays?

**A:** Repeated insertion at the beginning (`insert(0, x)`) shows quadratic growth in execution time due to element shifting.

---

### Flashcard 2

**Q:** What is the time complexity of repeatedly appending elements to a Python list?

**A:** Amortized **O(1)** per append.

---

### Flashcard 3

**Q:** Why does inserting at index 0 become slow as the list grows?

**A:** Every insertion shifts all existing elements one position to the right, resulting in **O(n)** time per insertion.

---

### Flashcard 4

**Q:** What happens to execution time when the input size for repeated front insertions is doubled?

**A:** The execution time increases by approximately four times, indicating **O(n²)** complexity.

---

### Flashcard 5

**Q:** Which searching algorithm is much faster on large sorted datasets?

**A:** Binary Search.

---

### Flashcard 6

**Q:** How does naive (linear) search compare with binary search experimentally?

**A:** Naive search takes significantly longer because it scans every element, while binary search examines only **O(log n)** elements.

---

### Flashcard 7

**Q:** Are NumPy arrays always faster than Python lists for searching and sorting?

**A:** No. Experiments show that Python lists often outperform NumPy arrays for indexing-heavy algorithms.

---

### Flashcard 8

**Q:** How does Selection Sort behave on different input orders?

**A:** It performs nearly the same on random, ascending, and descending inputs.

---

### Flashcard 9

**Q:** What is the time complexity of Merge Sort?

**A:** **O(n log n)**.

---

### Flashcard 10

**Q:** Why is Merge Sort still practical for very large datasets?

**A:** Because its **O(n log n)** complexity scales much better than quadratic sorting algorithms.

---

### Flashcard 11

**Q:** Why might NumPy arrays perform slower than Python lists in searching and sorting experiments?

**A:** NumPy introduces additional overhead designed for numerical and matrix operations rather than simple indexing.

---

### Flashcard 12

**Q:** When should Python lists generally be preferred?

**A:** For ordinary sequence manipulation, searching, sorting, and general-purpose programming.

---

### Flashcard 13

**Q:** When are NumPy arrays the better choice?

**A:** For numerical computations, matrix operations, and multidimensional data processing.

---

# Practice Quiz

## Multiple Choice Questions

### Q1.

The experiment of repeatedly calling `append()` demonstrates that its amortized complexity is:

A. O(n)

B. O(log n)

C. O(1)

D. O(n²)

**Answer:** C

---

### Q2.

Repeatedly inserting elements at the beginning of a Python list results in:

A. O(1)

B. O(log n)

C. O(n)

D. O(n²)

**Answer:** D

---

### Q3.

Which searching algorithm performs much faster on sorted data?

A. Linear Search

B. Binary Search

C. Selection Sort

D. Bubble Sort

**Answer:** B

---

### Q4.

Which data structure generally performed better for searching and sorting experiments?

A. NumPy arrays

B. Python lists

C. Linked lists

D. Dictionaries

**Answer:** B

---

### Q5.

Merge Sort has a time complexity of:

A. O(n²)

B. O(n)

C. O(log n)

D. O(n log n)

**Answer:** D

---

### Q6.

NumPy arrays are primarily optimized for:

A. String processing

B. Numerical and matrix computations

C. Dictionary lookups

D. File handling

**Answer:** B

---

## Short Answer Questions

### Q1.

How do the experiments confirm that Python lists are implemented as dynamic arrays?

**Answer:**

Repeated insertion at the beginning causes quadratic execution time because each insertion shifts existing elements. This behavior matches dynamic arrays rather than linked lists.

---

### Q2.

Why doesn't NumPy always outperform Python lists in searching and sorting?

**Answer:**

NumPy is optimized for numerical and matrix operations. For algorithms relying mainly on indexing, the additional overhead makes NumPy arrays slower than Python lists.

---

### Q3.

What is the main lesson from comparing Python lists and NumPy arrays?

**Answer:**

The best data structure depends on the application. Python lists are efficient for general sequence operations, while NumPy arrays are more suitable for scientific computing and matrix-based computations.