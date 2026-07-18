# Lecture 03: Implementation of Quicksort Algorithm

> **Course:** Programming, Data Structures and Algorithms using Python
>
> **Week:** 3
>
> **Lecture:** 2

---

# Lecture Notes

## Overview

In the previous lecture, we studied the **Quicksort algorithm** theoretically and analyzed its best, average, and worst-case time complexities.

This lecture focuses on the **practical implementation and performance evaluation** of Quicksort. Similar to earlier experiments with Selection Sort, Insertion Sort, and Merge Sort, we compare Quicksort's execution time on different kinds of input.

---

# Timer Utility

To measure execution time, the same **Timer class** used in previous experiments is reused.

It provides two operations:

- `start()` — starts the timer.
- `stop()` — stops the timer and reports elapsed execution time.

This allows practical comparison between different sorting algorithms.

---

# Increasing Python's Recursion Limit

Quicksort is implemented **recursively**.

Python has a default recursion depth of roughly **1000 recursive calls**, which is too small for very large inputs.

Therefore, before running Quicksort on large arrays, the recursion limit is increased.

```python
import sys
sys.setrecursionlimit(2**31 - 1)
```

This sets the recursion limit to the maximum value allowed by Python.

---

# Review of Quicksort Implementation

The implementation follows the algorithm discussed previously.

Steps:

1. Choose the **first element** as the pivot.
2. Partition the remaining elements into:
   - Elements smaller than the pivot.
   - Elements larger than the pivot.
3. Move the pivot into its correct position.
4. Recursively sort:
   - Left partition
   - Right partition

The recursive calls continue until subarrays contain zero or one element.

---

# In-place Sorting

The implemented Quicksort performs an **in-place sort**.

Although the function returns the sorted list, the original list is also modified because sorting is done by swapping elements within the same array.

For example:

```python
qnew = quicksort(qlist)
```

After execution:

- `qnew` contains the sorted list.
- `qlist` itself is also sorted.

No separate array is created.

---

# Worst Case of Quicksort

The lecture revisits the main weakness of Quicksort.

The algorithm always selects the **first element as pivot**.

If the first element happens to be:

- the smallest element, or
- the largest element,

the partition becomes:

- one empty subarray
- one subarray containing **n−1 elements**

Instead of dividing the problem approximately in half, the recursion becomes highly unbalanced.

Example:

```
Pivot | Remaining Elements

1 | 2 3 4 5 6 7
```

Recursive calls become:

```
n
n−1
n−2
...
1
```

leading to

```
O(n²)
```

time complexity.

---

# Experimental Comparison

The lecture compares Quicksort with Merge Sort.

Both algorithms are divide-and-conquer algorithms.

However,

- Merge Sort guarantees **O(n log n)** in every case.
- Quicksort has:
  - Best case: O(n log n)
  - Average case: O(n log n)
  - Worst case: O(n²)

The objective is to see how they behave **in practice**.

---

# Test Input

A large random array is generated.

```
Size = 10^6 elements
```

This is much larger than the datasets used for Selection Sort and Insertion Sort.

Ascending and descending inputs are also generated for Merge Sort because Merge Sort performs uniformly regardless of input order.

---

# Experimental Results

## Quicksort

Random input of size:

```
10^6
```

Execution time:

Approximately

```
7 seconds
```

---

## Merge Sort

Same random input:

```
10^6
```

Execution time:

Approximately

```
10 seconds
```

(about 50% slower than Quicksort on random input)

---

# Why is Quicksort Faster?

Although Merge Sort has a stronger theoretical guarantee, Quicksort usually performs faster in practice because:

- partitioning requires relatively little overhead
- operations occur mostly within the same array
- excellent cache performance
- fewer memory allocations

Merge Sort, on the other hand,

- repeatedly creates new arrays during merging
- copies many elements
- requires additional memory

These extra operations increase running time despite having the same asymptotic average complexity.

---

# Practical Observation

The experiment confirms an important idea in algorithm analysis:

Two algorithms with the same asymptotic complexity

```
O(n log n)
```

may still have noticeably different running times.

Constant factors and memory usage matter significantly in real implementations.

---

# Key Takeaways

- Quicksort is implemented recursively.
- Python's recursion limit must be increased for very large inputs.
- The implementation performs **in-place sorting**.
- Worst-case partitioning occurs when the pivot is the smallest or largest element.
- Random inputs usually produce balanced partitions.
- On random datasets, Quicksort is typically faster than Merge Sort.
- Merge Sort guarantees O(n log n), whereas Quicksort guarantees it only on average.
- Practical performance depends not only on asymptotic complexity but also on implementation overhead.

---

# Summary

This lecture validates the theoretical discussion of Quicksort through experiments.

Although Quicksort has an O(n²) worst case, it performs extremely well on random data and often outperforms Merge Sort in practice. Merge Sort remains asymptotically safer because it guarantees O(n log n) regardless of input, but Quicksort's lower practical overhead makes it one of the most widely used sorting algorithms.

---

# Flashcards

### Flashcard 1

**Q:** Why is Python's recursion limit increased before running Quicksort?

**A:** Because Quicksort is recursive and large inputs exceed Python's default recursion depth.

---

### Flashcard 2

**Q:** Is the implemented Quicksort in-place?

**A:** Yes. It modifies the original list by swapping elements.

---

### Flashcard 3

**Q:** Which pivot is used in this implementation?

**A:** The first element of the current subarray.

---

### Flashcard 4

**Q:** When does Quicksort exhibit its worst-case performance?

**A:** When the pivot is always the smallest or largest element, creating highly unbalanced partitions.

---

### Flashcard 5

**Q:** What is Quicksort's average-case complexity?

**A:** O(n log n)

---

### Flashcard 6

**Q:** What is Quicksort's worst-case complexity?

**A:** O(n²)

---

### Flashcard 7

**Q:** What is Merge Sort's worst-case complexity?

**A:** O(n log n)

---

### Flashcard 8

**Q:** Which algorithm was experimentally faster on large random inputs?

**A:** Quicksort.

---

### Flashcard 9

**Q:** Why can Quicksort be faster despite having a worse worst case?

**A:** Because it has lower practical overhead and better memory/cache performance.

---

### Flashcard 10

**Q:** Does asymptotic complexity always predict actual running time?

**A:** No. Constant factors and implementation details also affect performance.

---

# Practice Quiz

## Multiple Choice Questions

### Q1.

Why is Python's recursion limit increased before executing Quicksort?

A. To reduce memory usage

B. To improve sorting accuracy

C. To allow deep recursive calls on large inputs

D. To avoid creating extra arrays

**Answer:** C

---

### Q2.

The Quicksort implementation discussed selects which pivot?

A. Middle element

B. Random element

C. First element

D. Last element

**Answer:** C

---

### Q3.

The implemented Quicksort is:

A. Out-of-place

B. Stable

C. In-place

D. Iterative

**Answer:** C

---

### Q4.

On random inputs, Quicksort experimentally performed:

A. Slower than Merge Sort

B. Faster than Merge Sort

C. Exactly the same

D. Failed because of recursion

**Answer:** B

---

### Q5.

Merge Sort is slower in practice mainly because:

A. It is O(n²)

B. It repeatedly creates new arrays during merging

C. It cannot handle random inputs

D. It performs repeated comparisons of the pivot

**Answer:** B

---

## Short Answer Questions

### Q1.

Why does Quicksort's worst case occur when the pivot is the smallest or largest element?

**Answer:**
Because each partition becomes one empty subarray and one subarray of size n−1, leading to highly unbalanced recursion and O(n²) time.

---

### Q2.

Why can Quicksort outperform Merge Sort even though Merge Sort has a better worst-case guarantee?

**Answer:**
Quicksort has lower implementation overhead, performs in-place sorting, and has better cache performance, making it faster on average despite its O(n²) worst case.l