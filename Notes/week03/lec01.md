# Lecture 01: Quicksort

> **Course:** Programming, Data Structures and Algorithms
>
> **Week:** 3
>
> **Lecture:** 1

---

## Why Do We Need Another Sorting Algorithm?

So far, we have studied:

- Selection Sort → **O(n²)**
- Insertion Sort → **O(n²)**
- Merge Sort → **O(n log n)**

Merge Sort solves the performance problem of the naive sorting algorithms, but it still has two major drawbacks:

1. **Requires extra memory**
   - During merging, a completely new list is created.
   - Extra space of **O(n)** is required.

2. **Recursive implementation**
   - Merge Sort is naturally recursive.
   - Recursive function calls introduce overhead due to stack management.
   - Although recursion makes the algorithm elegant, it can reduce practical performance.

Therefore, we want a sorting algorithm that:

- Works close to **O(n log n)** time.
- Does **not require an extra array**.
- Can be implemented **in-place**.

This leads to **Quicksort**.

---

# Main Idea Behind Quicksort

The problem with Merge Sort is **merging**.

Suppose after sorting we obtain:

Left Half

```
1 3 5
```

Right Half

```
2 4 6
```

Although both halves are individually sorted,

```
1 3 5 | 2 4 6
```

is **not globally sorted**.

We must perform an expensive **merge** operation.

---

## What if we divided the list differently?

Instead of dividing by **position**, suppose we divide by **value**.

Imagine we somehow split the array so that:

```
All smaller elements | All larger elements
```

Example:

```
3 2 1 | 8 9 7
```

Every element on the left is smaller than every element on the right.

Now,

If we sort the left part:

```
1 2 3
```

and sort the right part:

```
7 8 9
```

the final array automatically becomes

```
1 2 3 7 8 9
```

No merge step is needed.

This is the central idea of Quicksort.

---

# Using the Median (Ideal Situation)

Suppose we know the **median** of the list.

The median divides the data into two equal halves:

- Half the elements are smaller.
- Half the elements are larger.

Example:

```
8 2 5 9 1 6 3
```

Median:

```
5
```

Partition:

```
2 1 3 | 5 | 8 9 6
```

Now:

- Left half has only smaller elements.
- Right half has only larger elements.

After recursively sorting:

```
1 2 3 | 5 | 6 8 9
```

No merging is required.

---

## Complexity if Median Were Free

If the median were magically available,

Each recursive call would:

- Partition the array → **O(n)**
- Solve two subproblems of size **n/2**

Recurrence:

```
T(n) = 2T(n/2) + O(n)
```

We already solved this recurrence during Merge Sort.

Therefore,

```
T(n) = O(n log n)
```

This would be perfect.

---

# Why Don't We Use the Median?

Because finding the median itself is difficult.

One simple way is:

1. Sort the array.
2. Pick the middle element.

But...

Sorting is exactly the problem we're trying to solve.

So we'd be sorting the array just to sort the array.

This becomes circular reasoning.

Hence, Quicksort does **not** use the median.

Instead, it uses something much cheaper.

---

# Pivot Element

Rather than finding the perfect median,

Quicksort simply chooses **any element**.

This chosen element is called the **pivot**.

Usually,

- First element
- Last element
- Random element
- Middle element

may be selected.

The lecture assumes the **first element** is chosen.

Example:

```
43 32 78 22 63 57 91 13
```

Pivot:

```
43
```

Now classify every element.

Smaller than pivot:

```
32 22 13
```

Larger than pivot:

```
78 63 57 91
```

After partitioning,

```
32 22 13 | 43 | 78 63 57 91
```

Notice:

Every value on the left is smaller than the pivot.

Every value on the right is larger than the pivot.

Therefore,

- Sort left recursively.
- Sort right recursively.

Done.

No merge operation is required.

---

# High-Level Quicksort Algorithm

```
Choose a pivot.

Partition the array into:

    Smaller elements
    Pivot
    Larger elements

Recursively sort:

    Left partition
    Right partition
```

Unlike Merge Sort,

there is **no merge step** after recursion.

The recursive calls become completely independent.

# Partitioning — The Heart of Quicksort

The most important step in Quicksort is **partitioning**.

Choosing the pivot is easy.

Recursively sorting the two partitions is also straightforward.

The difficult part is **rearranging the elements** so that:

```
All elements ≤ Pivot | Pivot | All elements > Pivot
```

If partitioning is done correctly, the rest of Quicksort works automatically.

---

# Partitioning Strategy Used in the Lecture

Assume the **first element is always the pivot**.

Initially, divide the array conceptually into four regions.

```
Pivot | Lower | Upper | Unclassified
```

where

- **Pivot** → fixed first element
- **Lower** → elements known to be ≤ pivot
- **Upper** → elements known to be > pivot
- **Unclassified** → elements not examined yet

Initially,

only the pivot is fixed.

Everything else is unclassified.

Example

```
43 32 22 78 63 57 91 13
```

Conceptually,

```
43 | | | 32 22 78 63 57 91 13
```

---

# Two Moving Boundaries

Maintain two pointers.

```
Pivot | Lower | Upper | Unclassified
         ^
       lower

               ^
             upper
```

Initially,

```
lower = upper = first element after pivot
```

because no element has been classified.

---

# Processing Each Unclassified Element

At every step,

look at the **first unclassified element**.

There are only two possibilities.

---

## Case 1

Current element > Pivot

Example

```
Pivot = 43

Current = 78
```

Since it belongs to the upper partition,

we simply extend the upper region.

Before

```
43 | 32 22 | | 78 63 57
```

After

```
43 | 32 22 | 78 | 63 57
```

Nothing is swapped.

Only the boundary moves.

This is the easy case.

---

## Case 2

Current element ≤ Pivot

Example

```
Pivot = 43

Current = 13
```

This element belongs to the lower partition.

Naively,

we could shift the entire upper partition one place to the right.

But shifting many elements would make the algorithm slow.

Instead,

Quicksort performs **one swap**.

---

# Clever Swapping Trick

Suppose the partitions currently look like

```
43 | 32 22 | 78 63 57 | 13
```

Here,

```
13
```

should move into the lower partition.

Instead of shifting

```
78 63 57
```

we simply swap

```
13
```

with

```
78
```

Result

```
43 | 32 22 13 | 63 57 78
```

Notice:

- Lower partition has grown.
- Upper partition still contains only large elements.
- Only one swap was required.

This makes partitioning efficient.

---

# Why Does This Work?

Suppose

```
Lower

32 22
```

Upper

```
78 63 57
```

Current element

```
13
```

Swap

```
13 ↔ 78
```

Result

Lower

```
32 22 13
```

Upper

```
63 57 78
```

The order inside the upper partition changes,

but **Quicksort does not care**.

The only invariant that matters is

- everything in Lower ≤ Pivot
- everything in Upper > Pivot

The internal ordering will be fixed later through recursion.

---

# Dry Run

Input

```
43 32 22 78 63 57 91 13
```

Pivot

```
43
```

---

### Step 1

Current = 32

```
32 ≤ 43
```

Lower grows.

```
43 | 32 | | 22 78 63 57 91 13
```

---

### Step 2

Current = 22

```
22 ≤ 43
```

```
43 | 32 22 | | 78 63 57 91 13
```

---

### Step 3

Current = 78

```
78 > 43
```

Upper grows.

```
43 | 32 22 | 78 | 63 57 91 13
```

---

### Step 4

Current = 63

```
63 > 43
```

```
43 | 32 22 | 78 63 | 57 91 13
```

---

### Step 5

Current = 57

```
57 > 43
```

```
43 | 32 22 | 78 63 57 | 91 13
```

---

### Step 6

Current = 91

```
91 > 43
```

```
43 | 32 22 | 78 63 57 91 | 13
```

---

### Step 7

Current = 13

```
13 ≤ 43
```

Swap

```
13 ↔ 78
```

Result

```
43 | 32 22 13 | 63 57 91 78
```

All elements have now been classified.

---

# Final Step — Place the Pivot

Current arrangement

```
43 | 32 22 13 | 63 57 91 78
```

Pivot is still at the beginning.

It should lie between the lower and upper partitions.

Swap

```
43 ↔ 13
```

Final partition

```
13 32 22 | 43 | 63 57 91 78
```

Observe carefully.

Everything left of 43 is smaller.

Everything right of 43 is larger.

The left and right halves are **not sorted yet**.

But they are completely independent.

Now recursively apply Quicksort to

```
13 32 22
```

and

```
63 57 91 78
```

Eventually,

the fully sorted array becomes

```
13 22 32 43 57 63 78 91
```

---

# Key Invariant During Partitioning

Throughout the algorithm,

the following property is always maintained:

```
Pivot | Lower | Upper | Unclassified
```

where

- Lower contains only elements ≤ Pivot.
- Upper contains only elements > Pivot.
- Unclassified elements have not yet been examined.

Each iteration shrinks the unclassified region by one element.

Eventually,

there are no unclassified elements left,

and the pivot is placed between the two partitions.

## Key Takeaways

- Quicksort follows the **Divide and Conquer** paradigm.
- It works by selecting a **pivot** and partitioning the array into:
  - Elements ≤ pivot
  - Pivot
  - Elements > pivot
- After partitioning, the pivot is already in its correct sorted position.
- The algorithm recursively sorts the left and right partitions.
- Unlike Merge Sort, Quicksort does **not require merging** after recursion.
- Partitioning is performed **in-place**, making Quicksort memory efficient.
- The Lomuto partition scheme uses:
  - Pivot = last element
  - `lower` pointer for boundary of smaller elements
  - `upper` pointer for scanning
- Partition always requires a **single linear scan** of the array.
- Quicksort performance depends heavily on pivot selection.

---

## GATE / Exam-Oriented Points

### Important Facts

- Quicksort is a **Divide and Conquer** algorithm.
- Partition complexity = **O(n)**.
- Pivot reaches its **final sorted position** after partitioning.
- No merge operation is required after recursive calls.
- Average-case complexity:
  - **Θ(n log n)**
- Worst-case complexity:
  - **Θ(n²)**
- Best case occurs when pivot divides the array approximately in half.
- Worst case occurs when pivot is always the smallest or largest element.
- Space complexity (recursive stack):
  - Average: **O(log n)**
  - Worst: **O(n)**

### Frequently Asked Questions

**Q. Why is Quicksort usually faster than Merge Sort in practice?**

Because:
- Partitioning happens in-place.
- Better cache locality.
- No extra array is needed.

---

**Q. What determines Quicksort's performance?**

The balance of the partitions.

Balanced partitions → O(n log n)

Highly unbalanced partitions → O(n²)

---

**Q. Does Quicksort preserve the order of equal elements?**

No.

Standard Quicksort is **not stable**.

---

**Q. Is Quicksort in-place?**

Yes.

Except for recursion stack memory.

---

## Flashcards

### Flashcard 1

**Q:** Which algorithmic paradigm does Quicksort use?

**A:** Divide and Conquer.

---

### Flashcard 2

**Q:** What is the purpose of partitioning?

**A:** Place the pivot in its final sorted position and divide elements into two groups.

---

### Flashcard 3

**Q:** After partitioning, what is guaranteed?

**A:** Every element on the left is ≤ pivot and every element on the right is > pivot.

---

### Flashcard 4

**Q:** Which pivot is used in the Lomuto partition scheme?

**A:** The last element.

---

### Flashcard 5

**Q:** What does the `lower` pointer represent?

**A:** Boundary of elements known to be ≤ pivot.

---

### Flashcard 6

**Q:** What does the `upper` pointer do?

**A:** Scans the array from left to right.

---

### Flashcard 7

**Q:** How many passes are needed for partitioning?

**A:** One linear scan.

---

### Flashcard 8

**Q:** Why doesn't Quicksort require merging?

**A:** Partitioning itself separates elements correctly around the pivot.

---

### Flashcard 9

**Q:** Average-case time complexity?

**A:** Θ(n log n)

---

### Flashcard 10

**Q:** Worst-case time complexity?

**A:** Θ(n²)

---

### Flashcard 11

**Q:** When does the worst case occur?

**A:** When the pivot is always the smallest or largest element.

---

### Flashcard 12

**Q:** Is Quicksort stable?

**A:** No.

---

### Flashcard 13

**Q:** Is Quicksort in-place?

**A:** Yes (excluding recursion stack).

---

### Flashcard 14

**Q:** Which algorithm requires merging after recursive calls?

**A:** Merge Sort.

---

### Flashcard 15

**Q:** Which sorting algorithm usually performs better in practice?

**A:** Quicksort.

---

## Practice Quiz

### MCQ 1

Quicksort follows which algorithmic paradigm?

A. Greedy

B. Dynamic Programming

C. Divide and Conquer

D. Backtracking

**Answer:** C

---

### MCQ 2

Which element is chosen as pivot in the lecture's implementation?

A. First element

B. Middle element

C. Random element

D. Last element

**Answer:** D

---

### MCQ 3

Partitioning requires

A. O(log n)

B. O(n)

C. O(n²)

D. O(1)

**Answer:** B

---

### MCQ 4

After partitioning,

A. Entire array is sorted

B. Pivot reaches its final position

C. Left side is completely sorted

D. Right side is completely sorted

**Answer:** B

---

### MCQ 5

Quicksort requires merging after recursion.

A. True

B. False

**Answer:** False

---

### MCQ 6

Worst-case Quicksort complexity is

A. Θ(log n)

B. Θ(n)

C. Θ(n log n)

D. Θ(n²)

**Answer:** D

---

### MCQ 7

Average-case Quicksort complexity is

A. Θ(log n)

B. Θ(n)

C. Θ(n log n)

D. Θ(n²)

**Answer:** C

---

### MCQ 8

Which statement is TRUE?

A. Quicksort is stable

B. Merge Sort is in-place

C. Quicksort partitions in-place

D. Merge Sort does not merge

**Answer:** C

---

### MCQ 9

The recursive calls are made on

A. Entire array

B. Pivot only

C. Left and right partitions

D. Random subarrays

**Answer:** C

---

### MCQ 10

Quicksort performs poorly when

A. Pivot divides array equally

B. Pivot is always smallest or largest

C. Array has random values

D. Array contains duplicates

**Answer:** B

---

## Summary

Quicksort improves upon earlier sorting algorithms by using the Divide and Conquer strategy. Instead of repeatedly selecting the minimum element or inserting elements into a sorted prefix, it partitions the array around a pivot. After partitioning, the pivot is permanently placed in its correct position, and the algorithm recursively sorts the two independent partitions. Since partitioning is done in-place and no merging is required, Quicksort is generally faster than Merge Sort in practice despite sharing the same average-case complexity of Θ(n log n). However, poor pivot selection can lead to highly unbalanced partitions, resulting in the worst-case complexity of Θ(n²).