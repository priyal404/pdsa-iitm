# Lecture 02: Analysis of Quicksort

> **Course:** Programming, Data Structures and Algorithms using Python
>
> **Week:** 3
>
> **Lecture:** 2

---

# Lecture Notes

## Overview

In the previous lecture, we learned how **Quicksort** works using the divide-and-conquer approach. This lecture focuses on analyzing Quicksort to determine its time complexity under different scenarios.

The key factor influencing Quicksort's performance is **how well the chosen pivot divides the array** into two smaller parts.

---

## Review of Quicksort

Quicksort follows these steps:

1. Choose a pivot.
2. Partition the array around the pivot.
3. Move the pivot to its correct sorted position.
4. Recursively sort the left partition.
5. Recursively sort the right partition.

The efficiency of the algorithm depends almost entirely on how balanced these two partitions are.

---

## Time Required for Partitioning

The partition operation scans the array only once.

During this scan:

- Every element is compared with the pivot.
- Elements are moved to either the left or right partition.
- The pivot is finally placed in its correct position.

Therefore,

```
Partition Time = O(n)
```

where **n** is the size of the current subarray.

---

## Best Case Analysis

The ideal situation occurs when the pivot is the **median** of the array.

This divides the array into two nearly equal halves.

```
n

      pivot

n/2          n/2
```

Each recursive call sorts half the elements.

The recurrence relation becomes:

```
T(n) = 2T(n/2) + O(n)
```

This is identical to the recurrence for Merge Sort.

Solving the recurrence gives:

```
T(n) = O(n log n)
```

Thus,

**Best Case Complexity**

```
O(n log n)
```

---

## Worst Case Analysis

The worst case occurs when the pivot is either:

- the smallest element, or
- the largest element.

In this situation, one partition is empty while the other contains all remaining elements.

Example:

```
Pivot

1 | 2 3 4 5 6 7
```

Partitions become:

```
0 elements

n−1 elements
```

Instead of reducing the problem size by half, only one element is removed at each recursive call.

The recurrence becomes:

```
T(n) = T(n−1) + O(n)
```

Expanding,

```
T(n)
= T(n−1) + n

= T(n−2) + (n−1) + n

= ...

= n + (n−1) + (n−2) + ... + 1
```

Using the arithmetic series formula,

```
1 + 2 + ... + n

= n(n+1)/2
```

Therefore,

```
T(n) = O(n²)
```

---

## An Interesting Observation

Unlike Insertion Sort, where an already sorted array is the **best case**, Quicksort behaves exactly the opposite (when the first element is chosen as the pivot).

Suppose the array is already sorted:

```
1 2 3 4 5 6
```

The first element is always the smallest.

Each recursive call produces:

```
0 elements

n−1 elements
```

Again,

```
T(n) = T(n−1) + O(n)
```

Thus,

Already sorted input becomes the **worst case** for this implementation of Quicksort.

---

## Average Case Analysis

Although Quicksort has an O(n²) worst case, its average performance is much better.

The lecture states (without proof) that:

```
Average Case = O(n log n)
```

---

## Why Can We Compute the Average?

For sorting algorithms based on comparisons, the actual values are irrelevant.

For example,

```
1 2 3

and

10 20 30
```

behave identically because only their **relative order** matters.

Therefore, every input of size **n** can be viewed simply as a permutation of the numbers:

```
1,2,3,...,n
```

There are

```
n!
```

possible permutations.

Assuming each permutation is equally likely, we can calculate the expected running time over all permutations.

The result is:

```
Average Case = O(n log n)
```

This means the O(n²) inputs are relatively rare.

---

## Why Fixed Pivot Selection is a Problem

Suppose the pivot is always chosen as:

- first element
- last element
- middle element

An adversary can always construct an input that forces the pivot to be the smallest or largest element at every recursive step.

Therefore, **any fixed pivot selection strategy has a corresponding worst-case input**.

---

## Randomized Pivot Selection

A better strategy is to choose the pivot randomly.

Instead of selecting a fixed position,

Generate a random index between

```
0

and

n−1
```

Every index has equal probability:

```
1/n
```

of being selected.

The chosen element becomes the pivot for that recursive call.

---

## Why Randomization Helps

Randomization makes it extremely difficult to consistently generate worst-case partitions.

Even if an adversary knows the input,

they cannot predict which pivot will be selected.

As a result,

balanced partitions occur much more frequently,

and the expected running time remains

```
O(n log n)
```

---

# Key Takeaways

- Partitioning always requires O(n) time.
- Best case occurs when the pivot divides the array into two equal halves.
- Best-case recurrence:
  ```
  T(n)=2T(n/2)+O(n)
  ```
- Best-case complexity:
  ```
  O(n log n)
  ```
- Worst case occurs when the pivot is the smallest or largest element.
- Worst-case recurrence:
  ```
  T(n)=T(n−1)+O(n)
  ```
- Worst-case complexity:
  ```
  O(n²)
  ```
- Already sorted arrays become the worst case when the first element is always chosen as the pivot.
- Average-case complexity is O(n log n).
- Choosing pivots randomly significantly reduces the chance of encountering the worst case.

---

# Summary

The performance of Quicksort depends entirely on the quality of its partitions. Balanced partitions lead to O(n log n) performance, while extremely unbalanced partitions lead to O(n²). Although the worst case exists, it occurs relatively infrequently. By selecting pivots randomly instead of using a fixed rule, Quicksort achieves O(n log n) expected running time and remains one of the fastest practical sorting algorithms.

---

# Flashcards

### Flashcard 1

**Q:** What operation dominates the running time of Quicksort?

**A:** Partitioning and the recursive sorting of partitions.

---

### Flashcard 2

**Q:** How much time does one partition operation take?

**A:** O(n)

---

### Flashcard 3

**Q:** When does Quicksort achieve its best-case performance?

**A:** When the pivot is approximately the median, creating two equal partitions.

---

### Flashcard 4

**Q:** What is the best-case recurrence relation?

**A:** T(n) = 2T(n/2) + O(n)

---

### Flashcard 5

**Q:** What is the best-case time complexity of Quicksort?

**A:** O(n log n)

---

### Flashcard 6

**Q:** When does the worst case occur?

**A:** When the pivot is always the smallest or largest element.

---

### Flashcard 7

**Q:** What is the worst-case recurrence?

**A:** T(n) = T(n−1) + O(n)

---

### Flashcard 8

**Q:** What is the worst-case complexity?

**A:** O(n²)

---

### Flashcard 9

**Q:** What is the average-case complexity?

**A:** O(n log n)

---

### Flashcard 10

**Q:** Why is randomized pivot selection preferred?

**A:** It greatly reduces the probability of consistently producing worst-case partitions.

---

# Practice Quiz

## Multiple Choice Questions

### Q1.

The partition step in Quicksort takes:

A. O(1)

B. O(log n)

C. O(n)

D. O(n²)

**Answer:** C

---

### Q2.

The best case for Quicksort occurs when:

A. The pivot is the smallest element.

B. The pivot is the largest element.

C. The pivot divides the array into nearly equal halves.

D. The array is already sorted.

**Answer:** C

---

### Q3.

The worst-case recurrence relation for Quicksort is:

A. T(n)=2T(n/2)+n

B. T(n)=T(n−1)+n

C. T(n)=T(log n)+1

D. T(n)=n/2

**Answer:** B

---

### Q4.

If the first element is always chosen as the pivot, an already sorted array results in:

A. Best case

B. Average case

C. Worst case

D. Constant time

**Answer:** C

---

### Q5.

Randomized pivot selection improves Quicksort because:

A. It guarantees balanced partitions.

B. It removes recursion.

C. It reduces the probability of consistently encountering the worst case.

D. It makes partitioning O(log n).

**Answer:** C

---

## Short Answer Questions

### Q1.

Why does Quicksort become O(n²) in the worst case?

**Answer:**
Because each partition contains one empty subarray and one subarray of size n−1, reducing the problem by only one element at each recursive call.

---

### Q2.

Why is the average-case analysis based on permutations rather than actual values?

**Answer:**
Because comparison-based sorting depends only on the relative ordering of elements, not on their actual values. Therefore, every input can be viewed as a permutation of 1 to n.