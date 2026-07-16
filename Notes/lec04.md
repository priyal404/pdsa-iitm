# Lecture 4: Searching in a List

> **Course:** Programming, Data Structures and Algorithms
>
> **Week:** 2
>
> **Lecture:** 4

---

# Introduction

Searching is one of the most fundamental problems in computer science.

Given a collection of elements and a target value, we want to determine whether the target exists in the collection.

Although the problem appears simple, the efficiency of the solution depends heavily on the structure of the data.

If the data is completely unsorted, we have very limited options. However, if the data is sorted, we can exploit this ordering to search much more efficiently.

This lecture compares two important searching algorithms:

- **Linear Search**
- **Binary Search**

---

# The Search Problem

The problem can be stated as follows:

> Given a value $v$ and a list $L$, determine whether $v$ is present in the list.

The algorithm only needs to answer one of two possibilities:

- **True** — the value exists.
- **False** — the value does not exist.

---

# Linear Search

When no information is available about the ordering of the list, the safest approach is to examine every element one by one.

Pseudo-code:

```text
for each element x in L:
    if x == v:
        return True

return False
```

The search stops immediately when the target value is found.

If the entire list is scanned without finding the target, the algorithm returns `False`.

---

# Why Is This the Only Choice?

Suppose the list is

```text
[23, 5, 91, 18, 42]
```

and we are searching for

```text
42
```

Since the values are arranged randomly, there is no information that allows us to skip any element.

The value could appear

- at the beginning,
- in the middle,
- at the end,
- or may not exist at all.

Therefore, every element is a potential candidate and may need to be examined.

---

# Complexity Analysis

Let

$$
n=\text{length of the list}.
$$

In the worst case,

the algorithm compares the target with every element exactly once.

Therefore,

$$
T(n)=O(n).
$$

---

# Best Case vs Worst Case

### Best Case

The target is the first element.

```text
[15, 7, 10, 22]
 ^
```

Only one comparison is required.

Complexity:

$$
O(1).
$$

---

### Worst Case

The target is

- the last element, or
- absent from the list.

Example:

```text
[15, 7, 10, 22]
```

Searching for

```text
50
```

requires examining every element.

Complexity:

$$
O(n).
$$

---

# Limitation of Linear Search

As the size of the list grows, the number of comparisons grows proportionally.

Searching through a list containing one million elements may require nearly one million comparisons in the worst case.

This motivates the search for a more efficient algorithm.

---

# Using a Sorted List

Suppose the list is arranged in ascending order.

Example:

```text
[3, 8, 15, 24, 39, 45, 60]
```

Now consider searching for

```text
24.
```

Instead of examining every element, we can exploit the ordering of the list.

This idea leads to **Binary Search**.

---

# Key Idea Behind Binary Search

Binary Search repeatedly divides the search space into two halves.

At every step,

1. Find the middle element.
2. Compare it with the target.
3. Eliminate the half that cannot possibly contain the target.
4. Continue searching in the remaining half.

Since half of the remaining elements are discarded after every comparison, the search becomes extremely efficient.

---

# Binary Search Algorithm

Assume the list is sorted in ascending order.

The algorithm works as follows.

1. Compute the middle position.
2. Compare the middle element with the target.
3. If they are equal, return `True`.
4. If the target is smaller, search the left half.
5. If the target is larger, search the right half.
6. Repeat until the search interval becomes empty.

---

# Recursive Implementation

A recursive implementation naturally expresses this repeated division.

```text
BinarySearch(L, v)

if L is empty:
    return False

m = middle index

if L[m] == v:
    return True

if v < L[m]:
    search left half

else:
    search right half
```

Each recursive call works on only one half of the previous search interval.

---

# Why Can We Discard Half the List?

Suppose the sorted list is

```text
[4, 9, 15, 23, 41, 56, 70]
```

The middle element is

```text
23
```

If we are searching for

```text
56,
```

then every element before 23 is guaranteed to be smaller than 23.

Since

$$
56>23,
$$

the entire left half can be ignored immediately.

Similarly, if we were searching for

```text
15,
```

the entire right half could be discarded.

This elimination is possible **only because the list is sorted**.

---

# Search Interval

Binary Search never examines the whole list after the first comparison.

Instead, it repeatedly reduces the **search interval**.

Initially,

```text
Entire list
```

After one comparison,

```text
Half of the list
```

After two comparisons,

```text
One-fourth of the list
```

After three comparisons,

```text
One-eighth of the list
```

This repeated halving continues until either the target is found or no elements remain.

---

# Empty List as the Base Case

Eventually, the search interval becomes empty.

An empty list clearly cannot contain the target value.

Therefore,

the recursion stops by returning

```text
False
```

This forms the base case of the recursive algorithm.

---

# Computing the Midpoint

The midpoint divides the current search interval into two nearly equal halves.

If the interval contains

$$
n
$$

elements,

the midpoint is approximately

$$
\left\lfloor\frac{n}{2}\right\rfloor.
$$

In Python,

integer division is commonly used:

```python
mid = len(L) // 2
```

This guarantees that the midpoint is always a valid index.

---

# Why Binary Search Is Faster

Suppose we begin with

$$
1024
$$

elements.

After each comparison, the remaining search space becomes

| Comparison | Remaining Elements |
|------------|-------------------:|
| Start | 1024 |
| 1 | 512 |
| 2 | 256 |
| 3 | 128 |
| 4 | 64 |
| 5 | 32 |
| 6 | 16 |
| 7 | 8 |
| 8 | 4 |
| 9 | 2 |
| 10 | 1 |

Only **10 comparisons** are needed to reduce a list of 1024 elements to a single candidate.

This dramatic reduction is what makes Binary Search significantly more efficient than Linear Search.

# Complexity Analysis of Binary Search

Unlike Linear Search, Binary Search repeatedly reduces the search interval by half.

Instead of scanning every element, it focuses only on the half that can possibly contain the target value.

To determine its complexity, we examine how quickly the search interval shrinks.

Suppose the initial list contains

$$
n
$$

elements.

After one comparison, only half of the list remains.

After two comparisons,

$$
\frac{n}{4}
$$

elements remain.

Continuing this process, after $k$ comparisons, the size of the search interval becomes

$$
\frac{n}{2^k}.
$$

The search terminates when only one element remains.

Therefore,

$$
\frac{n}{2^k}=1.
$$

Solving for $k$,

$$
2^k=n,
$$

which gives

$$
k=\log_2 n.
$$

Ignoring the logarithm's base in asymptotic notation,

$$
T(n)=O(\log n).
$$

---

# Recurrence Relation for Binary Search

Binary Search is naturally recursive.

Each recursive call solves the same problem on a list that is only half as large as before.

Let

$$
T(n)
$$

represent the time required to search a list of size

$$
n.
$$

There are two possible cases.

### Base Case

If the list is empty,

the algorithm immediately returns `False`.

This requires only constant time.

$$
T(0)=1.
$$

---

### Recursive Case

For a non-empty list,

the algorithm performs a fixed number of operations:

- Compute the midpoint.
- Compare the middle element with the target.
- Decide whether to search the left or right half.

After these operations, the algorithm recursively searches only one half of the list.

Therefore,

$$
T(n)=T\left(\frac{n}{2}\right)+1.
$$

This equation is called the **recurrence relation** for Binary Search.

---

# Solving the Recurrence

We repeatedly substitute the recurrence into itself.

Starting with

$$
T(n)=T\left(\frac{n}{2}\right)+1,
$$

expand the recursive term.

$$
T\left(\frac{n}{2}\right)
=
T\left(\frac{n}{4}\right)+1.
$$

Substituting,

$$
T(n)
=
T\left(\frac{n}{4}\right)+2.
$$

Repeating once more,

$$
T(n)
=
T\left(\frac{n}{8}\right)+3.
$$

A clear pattern emerges.

After performing the substitution

$$
k
$$

times,

$$
T(n)
=
T\left(\frac{n}{2^k}\right)+k.
$$

---

# Reaching the Base Case

The recursion ends when

$$
\frac{n}{2^k}=1.
$$

Thus,

$$
k=\log_2 n.
$$

Substituting,

$$
T(n)
=
T(1)+\log_2 n.
$$

Evaluating the base case,

$$
T(1)
=
T(0)+1,
$$

which is a constant.

Therefore,

$$
T(n)
=
O(\log n).
$$

This confirms the result obtained from the intuitive halving argument.

---

# Intuitive vs Mathematical Analysis

There are two common ways to analyze Binary Search.

### Intuitive Method

Observe that every comparison eliminates half of the remaining search space.

The number of halvings required to reduce the interval to one element is

$$
\log n.
$$

---

### Recurrence Method

Write a recurrence describing the recursive calls.

$$
T(n)
=
T\left(\frac{n}{2}\right)+1.
$$

Solve the recurrence by repeated substitution.

Both approaches lead to exactly the same complexity.

The recurrence method is particularly useful because it applies to many recursive algorithms beyond Binary Search.

---

# Linear Search vs Binary Search

| Feature | Linear Search | Binary Search |
|---------|---------------|---------------|
| Data requirement | Unsorted or sorted | Must be sorted |
| Strategy | Scan every element | Repeatedly divide the search space |
| Worst-case complexity | $O(n)$ | $O(\log n)$ |
| Best-case complexity | $O(1)$ | $O(1)$ |
| Suitable for | Small or unsorted datasets | Large sorted datasets |

---

# Why Sorting Makes Such a Difference

Without any ordering, every element is equally likely to contain the target.

As a result,

no element can be safely ignored.

When the list is sorted,

a single comparison with the middle element immediately tells us which half cannot contain the target.

This ability to eliminate half the search space after every comparison is the key reason Binary Search is much faster.

---

# A Remarkable Improvement

Suppose a sorted list contains

$$
1,000,000
$$

elements.

Since

$$
\log_2(1,000,000)\approx20,
$$

Binary Search requires at most about **20 comparisons** to determine whether the target exists.

By contrast,

Linear Search may require examining all one million elements.

This dramatic improvement illustrates the power of choosing an efficient algorithm.

---

# Common Mistakes

### 1. Applying Binary Search to an Unsorted List

Binary Search assumes the data is sorted.

Without this property,

discarding half of the search space is not valid.

---

### 2. Confusing Linear and Logarithmic Growth

Linear Search examines elements one by one.

Binary Search reduces the remaining search space exponentially.

The difference becomes enormous for large datasets.

---

### 3. Ignoring the Base Case

Every recursive algorithm requires a stopping condition.

For Binary Search,

the recursion terminates when the search interval becomes empty.

---

### 4. Forgetting That Only One Recursive Call Is Made

Although Binary Search has two recursive branches in its code,

only **one** branch is followed during execution.

Hence the recurrence is

$$
T(n)=T\left(\frac{n}{2}\right)+1,
$$

and **not**

$$
2T\left(\frac{n}{2}\right)+1.
$$

This distinction is crucial.

---

# Key Takeaways

- Searching determines whether a target value exists in a collection.
- Linear Search works for any list but requires $O(n)$ time in the worst case.
- Binary Search requires the list to be sorted.
- Every comparison in Binary Search eliminates half of the remaining search interval.
- Binary Search satisfies the recurrence

$$
T(n)=T\left(\frac{n}{2}\right)+1.
$$

- Solving the recurrence gives

$$
T(n)=O(\log n).
$$

- Binary Search is one of the most efficient searching algorithms for sorted data.

---

# GATE / Interview Focus

- Binary Search **requires sorted input**.
- Worst-case complexity of Linear Search: $O(n)$.
- Worst-case complexity of Binary Search: $O(\log n)$.
- Binary Search halves the search space after every comparison.
- The recurrence for Binary Search is

$$
T(n)=T\left(\frac{n}{2}\right)+1.
$$

- Only one recursive call is executed at each step.

---

# Flashcards

**Q:** What is the worst-case complexity of Linear Search?

**A:** $O(n)$.

---

**Q:** What is the worst-case complexity of Binary Search?

**A:** $O(\log n)$.

---

**Q:** What property must the input satisfy for Binary Search?

**A:** The list must be sorted.

---

**Q:** What recurrence describes Binary Search?

**A:**

$$
T(n)=T\left(\frac{n}{2}\right)+1.
$$

---

**Q:** Why is Binary Search faster than Linear Search?

**A:** It discards half of the remaining search space after every comparison.

---

# Practice MCQs

### Q1

Which searching algorithm can be applied to an unsorted list?

A. Binary Search

B. Linear Search

C. Interpolation Search

D. Exponential Search

**Answer:** B

---

### Q2

The worst-case complexity of Binary Search is

A. $O(1)$

B. $O(\log n)$

C. $O(n)$

D. $O(n^2)$

**Answer:** B

---

### Q3

Binary Search repeatedly performs which operation?

A. Swapping adjacent elements

B. Dividing the search interval into two halves

C. Comparing every pair of elements

D. Traversing the list sequentially

**Answer:** B

---

### Q4

Which recurrence correctly represents Binary Search?

A. $T(n)=T(n-1)+1$

B. $T(n)=2T(n-1)+1$

C. $T(n)=T(n/2)+1$

D. $T(n)=2T(n/2)+1$

**Answer:** C

---

### Q5

Approximately how many comparisons are required to search one million sorted elements using Binary Search?

A. 20

B. 100

C. 1000

D. 1,000,000

**Answer:** A

---

# One-Page Revision

- **Linear Search**
  - Works on any list.
  - Scans elements sequentially.
  - Worst-case complexity: $O(n)$.

- **Binary Search**
  - Requires sorted data.
  - Compares with the middle element.
  - Eliminates half the search space after every comparison.
  - Worst-case complexity: $O(\log n)$.

- Binary Search recurrence:

$$
T(n)=T\left(\frac{n}{2}\right)+1.
$$

- Solution:

$$
T(n)=O(\log n).
$$

- Binary Search is significantly faster than Linear Search for large, sorted datasets.