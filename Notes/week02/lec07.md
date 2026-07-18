# Merge Sort

Merge Sort is a sorting algorithm based on the **Divide and Conquer** paradigm. Unlike Selection Sort and Insertion Sort, which repeatedly rearrange elements within a single list, Merge Sort repeatedly **divides** the list into smaller parts, sorts each part independently, and finally **merges** the sorted parts back together.

The motivation behind Merge Sort is to design an algorithm that performs significantly better than **O(n²)** for large inputs.

---

## Divide and Conquer Strategy

The algorithm works in three steps:

1. Divide the list into two equal halves.
2. Recursively sort each half.
3. Merge the two sorted halves into one sorted list.

The key idea is that each half can be sorted **independently**, making the problem easier to solve recursively.

---

## Why Merge?

Imagine two teaching assistants independently sort two halves of a stack of exam papers.

```
TA 1 → Sorted Left Half

TA 2 → Sorted Right Half
```

Both halves are individually sorted, but the complete collection is still not sorted.

The final task is to **merge** these two sorted halves into one completely sorted list.

This merging step is the heart of Merge Sort.

---

# Merging Two Sorted Lists

Suppose we have two sorted lists:

```
A = [32, 74, 89]

B = [21, 55, 64]
```

To merge them:

- Compare the first elements.
- Move the smaller element into a new list.
- Advance only in the list from which the element was taken.
- Repeat until one list becomes empty.
- Copy the remaining elements of the other list.

### Example

Initial lists

```
A : 32 74 89

B : 21 55 64
```

Comparison sequence

```
21 vs 32 → 21

32 vs 55 → 32

55 vs 74 → 55

64 vs 74 → 64

74

89
```

Final merged list

```
21 32 55 64 74 89
```

At every step, only the **first unprocessed element** of each list needs to be compared.

---

# Merge Sort Example

Suppose the input is

```
43 32 78 22 57 13 91 63
```

---

### Step 1: Divide

```
43 32 78 22 | 57 13 91 63
```

Divide again

```
43 32 | 78 22 | 57 13 | 91 63
```

Divide until every sublist contains one element

```
43

32

78

22

57

13

91

63
```

A list with one element is already sorted.

---

### Step 2: Merge Small Lists

Merge adjacent single-element lists

```
43 32

↓

32 43
```

```
78 22

↓

22 78
```

```
57 13

↓

13 57
```

```
91 63

↓

63 91
```

---

### Step 3: Merge Larger Lists

Merge the sorted pairs

```
32 43

22 78

↓

22 32 43 78
```

```
13 57

63 91

↓

13 57 63 91
```

---

### Step 4: Final Merge

Merge the two sorted halves

```
22 32 43 78

13 57 63 91
```

↓

```
13 22 32 43 57 63 78 91
```

The entire list is now sorted.

---

# Why Merge Sort Works

Merge Sort repeatedly solves **smaller versions of the same problem**.

Instead of sorting eight elements directly,

```
Sort 8 elements
```

becomes

```
Sort 4 + Sort 4
```

Each becomes

```
Sort 2 + Sort 2
```

Each becomes

```
Sort 1 + Sort 1
```

Since a single element is already sorted, recursion eventually reaches the base case.

The sorted pieces are then merged back together until the entire list becomes sorted.

---

# Merge Procedure

Assume

- List **A** has length **m**
- List **B** has length **n**

Maintain three indices:

- `i` → current position in A
- `j` → current position in B
- `k` → current position in output list C

Initially,

```python
i = 0
j = 0
k = 0
C = []
```

Repeatedly compare

```
A[i]
```

and

```
B[j]
```

Move the smaller element into `C` and increment the corresponding index.

Special cases:

- If A becomes empty, copy the remaining elements of B.
- If B becomes empty, copy the remaining elements of A.

The process stops after

```
m + n
```

elements have been copied.

---

## Merge Function (Python)

```python
def merge(A, B):
    (m, n) = (len(A), len(B))
    (C, i, j, k) = ([], 0, 0, 0)

    while k < m + n:
        if i == m:
            C.extend(B[j:])
            k += (n - j)

        elif j == n:
            C.extend(A[i:])
            k += (m - i)

        elif A[i] < B[j]:
            C.append(A[i])
            (i, k) = (i + 1, k + 1)

        else:
            C.append(B[j])
            (j, k) = (j + 1, k + 1)

    return C
```

---

# Merge Sort Algorithm

The recursive algorithm is remarkably simple.

If the list contains zero or one element,

- it is already sorted.

Otherwise,

1. Divide the list into two halves.
2. Sort each half recursively.
3. Merge the two sorted halves.

---

## Merge Sort (Python)

```python
def mergesort(L):
    if len(L) <= 1:
        return L

    mid = len(L) // 2

    left = mergesort(L[:mid])
    right = mergesort(L[mid:])

    return merge(left, right)
```

---

# Base Case

The recursion stops when

```python
len(L) <= 1
```

A list containing zero or one element is already sorted.

No further work is required.

---

# Recursive Structure

```
MergeSort(List)

↓

Split

↓

MergeSort(Left)

MergeSort(Right)

↓

Merge(Left, Right)

↓

Sorted List
```

The same algorithm is repeatedly applied until the smallest possible problem is reached.

---

# Key Points

- Merge Sort follows the **Divide and Conquer** paradigm.
- The list is repeatedly divided into two halves.
- Each half is sorted independently.
- The merge operation combines two sorted lists into one sorted list.
- Merging requires comparing only the first unprocessed elements of both lists.
- The recursion stops when every sublist contains a single element.
- Merge Sort is much more efficient than Selection Sort and Insertion Sort for large inputs.

---

# Summary

- **Strategy:** Divide and Conquer
- Divide the list into two equal halves.
- Recursively sort each half.
- Merge the sorted halves.
- Base case: list size ≤ 1.
- The merge operation is the core of the algorithm.
- Merge Sort improves upon the **O(n²)** algorithms studied earlier.
- The exact time complexity analysis will be covered separately.