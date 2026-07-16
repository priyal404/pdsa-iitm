## Recursive Insertion Sort

Insertion sort can also be written recursively. Instead of repeatedly expanding the sorted prefix using loops, recursion assumes that a smaller portion of the list is already sorted and then inserts the remaining element into its correct position.

The recursive solution is built using two functions:

- `insert()` – inserts one element into an already sorted list.
- `insertionSort()` – recursively sorts the list by repeatedly calling `insert()`.

---

### Recursive `insert()` Function

Suppose the list is already sorted, and we want to insert a value `v`.

There are three cases:

1. **Empty list**
   - If the list is empty, simply return a new list containing `v`.
   - This is the base case.

2. **`v` belongs at the end**
   - If `v` is greater than or equal to the last element, append it.
   - The list remains sorted.

3. **`v` belongs somewhere before the last element**
   - Temporarily remove the last element.
   - Recursively insert `v` into the remaining sorted portion.
   - Append the removed element back.

This effectively moves backward through the list until the correct insertion point is found.

### Recursive `insert()` (Python)

```python
def insert(L, v):
    if len(L) == 0:
        return [v]

    if v >= L[-1]:
        return L + [v]

    return insert(L[:-1], v) + [L[-1]]
```

---

### Recursive Insertion Sort

The recursive sorting algorithm follows a simple idea:

- If the list is empty, it is already sorted.
- Otherwise:
  1. Recursively sort all elements except the last.
  2. Insert the last element into the sorted sublist.

### Recursive Insertion Sort (Python)

```python
def insertionSort(L):
    if len(L) < 1:
        return L

    return insert(insertionSort(L[:-1]), L[-1])
```

This follows the divide-and-build strategy:

- First solve a smaller problem.
- Then combine the result by inserting the final element into its correct position.

---

## In-place vs Recursive Version

There is an important distinction between the iterative and recursive implementations.

### Iterative Version

- Modifies the original list directly.
- Uses swaps to move elements.
- Requires no additional list.
- **In-place algorithm.**

### Recursive Version

- Creates new lists during recursion.
- Does **not** modify the original list.
- Returns a completely new sorted list.

Python itself provides both approaches:

```python
L.sort()      # Sorts the original list (in-place)

sorted(L)     # Returns a new sorted list
```

---

# Time Complexity Analysis (Iterative)

Correctness follows from the invariant:

> Before every iteration, the prefix `L[0:i]` is already sorted.

Each iteration inserts one new element into this sorted prefix.

---

### Outer Loop

Runs once for every element.

```
n iterations
```

---

### Inner Loop

To insert the `i`th element, we may need to compare it with every previous element.

Worst case:

```
i comparisons
```

---

### Total Work

```
0 + 1 + 2 + ... + (n-1)
```

Using the summation formula,

\[
0+1+2+\cdots+(n-1)=\frac{n(n-1)}{2}
\]

Ignoring constants and lower-order terms,

\[
T(n)=O(n^2)
\]

---

## Time Complexity Analysis (Recursive)

Let:

- `Ti(n)` = time taken by `insert()`
- `Ts(n)` = time taken by `insertionSort()`

---

### Complexity of `insert()`

Base case:

```
Ti(0) = 1
```

Recursive case:

```
Ti(n) = Ti(n-1) + 1
```

Expanding,

```
Ti(n)
= Ti(n-1)+1
= Ti(n-2)+2
= ...
= Ti(0)+n
```

Therefore,

\[
Ti(n)=O(n)
\]

---

### Complexity of Recursive Insertion Sort

Base case:

```
Ts(0) = 1
```

Recursive case:

```
Ts(n)=Ts(n-1)+Ti(n-1)
```

Since

```
Ti(n-1)=O(n)
```

we get

```
Ts(n)
= 1 + 2 + 3 + ... + (n-1)
```

which becomes

\[
T(n)=O(n^2)
\]

Thus, both recursive and iterative insertion sort have the same worst-case complexity.

---

# Key Differences: Selection Sort vs Insertion Sort

| Selection Sort | Insertion Sort |
|---------------|---------------|
| Finds the minimum element repeatedly | Inserts the next element into the correct position |
| Uses repeated selection | Uses repeated insertion |
| Every pass scans the unsorted portion completely | Work depends on how far an element must move |
| Always performs roughly the same amount of work | Performance depends on the initial order of the input |
| Worst case: **O(n²)** | Worst case: **O(n²)** |

---

# Best-Case Behavior

Unlike selection sort, insertion sort can be much faster when the input is already nearly sorted.

For example:

```
5 6 7 8
```

Each new element is already greater than the previous one.

The inner loop terminates immediately, requiring only one comparison.

Thus the running time becomes approximately

\[
O(n)
\]

---

## Worst Case

If the list is in reverse order,

```
8 7 6 5
```

every new element must move all the way to the beginning.

The amount of work becomes

```
1 + 2 + 3 + ... + (n-1)
```

giving

\[
O(n^2)
\]

---

# Summary

- Recursive insertion sort is built using two recursive functions:
  - `insert()`
  - `insertionSort()`
- The iterative version modifies the original list, while the recursive version creates a new sorted list.
- Both recursive and iterative implementations have:
  - **Worst-case complexity:** **O(n²)**
- Insertion sort performs significantly better on nearly sorted data.
- Best case:
  - **O(n)**
- Worst case:
  - **O(n²)**
- Unlike selection sort, insertion sort's performance depends heavily on the initial arrangement of the input.