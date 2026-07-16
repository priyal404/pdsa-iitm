# Analysis of Merge Sort

## Merge Sort Recap

Merge Sort is based on the **Divide and Conquer** strategy.

### Steps
1. Divide the list into two equal halves.
2. Recursively sort the left half.
3. Recursively sort the right half.
4. Merge the two sorted halves into one sorted list.

---

# Analysis of Merge Function

Suppose:
- List **A** contains **m** elements.
- List **B** contains **n** elements.

During merging:
- Every element from both lists is copied exactly once into the output list.
- At least one element is moved in every iteration.
- The process continues until all **m + n** elements have been copied.

### Time Complexity

\[
T_{merge}(m,n)=O(m+n)
\]

Since Merge Sort usually merges two halves of approximately equal size,

- \(m \approx n/2\)
- Total elements = \(n\)

Therefore,

\[
\boxed{Merge = O(n)}
\]

---

# Recurrence Relation of Merge Sort

Let **T(n)** be the time required to sort **n** elements.

### Base Case

```
T(0) = 1
T(1) = 1
```

### Recursive Case

To sort **n** elements:

- Sort first half → **T(n/2)**
- Sort second half → **T(n/2)**
- Merge both halves → **O(n)**

Hence,

```
T(n) = 2T(n/2) + n
```

---

# Solving the Recurrence

Expand repeatedly:

```
T(n)
= 2T(n/2) + n

= 2²T(n/4) + 2n

= 2³T(n/8) + 3n

...

= 2ᵏT(n/2ᵏ) + kn
```

We stop when

```
n / 2ᵏ = 1
```

Therefore,

```
k = log₂n
```

Substituting,

```
T(n)
= 2^(log₂n) T(1) + n log₂n

= n + n log₂n
```

Ignoring lower-order terms,

> **Merge Sort = O(n log n)**

---

# Why Merge Sort is Better

Comparison:

| Algorithm | Worst Case |
|-----------|-----------|
| Selection Sort | O(n²) |
| Insertion Sort | O(n²) |
| Merge Sort | O(n log n) |

For large values of **n**,

```
n log n << n²
```

Therefore, Merge Sort is much more efficient than Selection Sort and Insertion Sort for large datasets.

---

# Advantages of Merge Sort

- Uses the **Divide and Conquer** strategy.
- Guaranteed **O(n log n)** time complexity.
- Efficient for large datasets.
- Stable sorting algorithm (preserves the order of equal elements).
- The merge procedure can also be used for:
  - Union of two sorted lists
  - Intersection of two sorted lists
  - Difference of two sorted lists
  - Removing duplicates

---

# Disadvantages of Merge Sort

### 1. Extra Space Required

- Merge operation creates a new temporary list.
- Cannot easily perform sorting completely in-place.

**Space Complexity**

```
O(n)
```

---

### 2. Recursive Nature

- Naturally implemented using recursion.
- Recursive calls add function-call overhead.
- Iterative implementation is possible but much more complicated.

---

# Complexity Summary

| Operation | Complexity |
|-----------|-----------|
| Merge | O(n) |
| Merge Sort | O(n log n) |
| Extra Space | O(n) |

---

# Comparison of Algorithms

| Algorithm | Best Case | Worst Case | Space |
|-----------|-----------|------------|-------|
| Linear Search | O(1) | O(n) | O(1) |
| Binary Search | O(1) | O(log n) | O(1) |
| Selection Sort | O(n²) | O(n²) | O(1) |
| Insertion Sort | O(n) | O(n²) | O(1) |
| Merge Sort | O(n log n) | O(n log n) | O(n) |

---

# Key Points

- Merge Sort follows the **Divide and Conquer** approach.
- The merge operation takes **O(n)** time.
- Recurrence relation:

```
T(n) = 2T(n/2) + n
```

- Solving the recurrence gives:

```
T(n) = O(n log n)
```

- Merge Sort is significantly faster than Selection Sort and Insertion Sort for large inputs.
- It requires **O(n)** additional memory because merging uses a temporary list.
- The merge technique is also useful for operations such as **union**, **intersection**, **difference**, and **duplicate removal** on sorted lists.