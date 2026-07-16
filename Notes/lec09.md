# Implementation of Searching and Sorting Algorithms

## Objective

This lecture demonstrates the practical implementation of the searching and sorting algorithms studied earlier. Instead of only analyzing theoretical complexities, the algorithms are executed on large inputs and their execution times are measured using Python.

---

# Measuring Execution Time

A custom **Timer** class is used to measure the execution time of algorithms.

The timer provides two basic operations:

- **start()** – starts the timer.
- **stop()** – stops the timer and reports the elapsed time.

This allows comparison of the actual running time of different algorithms.

---

# Comparing Searching Algorithms

Two searching algorithms are implemented:

1. **Naive (Linear) Search**
2. **Binary Search**

---

## Naive Search

The algorithm scans the list from beginning to end.

### Algorithm

- Compare each element with the target.
- If found, return **True**.
- If the entire list is scanned without finding the target, return **False**.

### Worst Case

Occurs when the element is **not present**.

**Time Complexity**

```
O(n)
```

---

## Binary Search

Binary Search repeatedly divides the search interval into two halves.

### Algorithm

1. Compare the target with the middle element.
2. If equal, return **True**.
3. If smaller, search the left half.
4. If larger, search the right half.

### Requirement

The list must be **sorted**.

### Worst Case

```
O(log n)
```

---

# Correctness Test

A sorted list containing all even numbers from **0 to 50** is created.

Each number from **0 to 50** is searched.

Expected results:

- Even numbers → Found (`True`)
- Odd numbers → Not Found (`False`)

This confirms that both implementations are correct before comparing their performance.

---

# Performance Comparison

### Experiment

- List size:

```
10⁵ elements
```

- Perform

```
10⁴ unsuccessful searches
```

using both algorithms.

Since the searched values are not present, both algorithms execute their **worst-case behavior**.

### Observed Results

| Algorithm | Approximate Time |
|------------|-----------------|
| Naive Search | 10.6 seconds |
| Binary Search | < 1 second |

### Observation

Binary Search is significantly faster because it reduces the search space by half at every step.

Although theoretical analysis predicts an even larger improvement, practical execution includes implementation overhead.

---

# Selection Sort Implementation

Selection Sort repeatedly finds the minimum element and places it at the beginning of the unsorted portion.

### Experiment

Three input lists of size **5000** are created:

- Random order
- Ascending order
- Descending order

Each list is sorted using Selection Sort.

### Results

| Input Order | Approximate Time |
|--------------|-----------------|
| Random | ~1.2 s |
| Ascending | ~1.2 s |
| Descending | ~1.2 s |

### Observation

Selection Sort performs almost identically regardless of the initial ordering.

This matches theoretical analysis because Selection Sort always scans the remaining unsorted elements completely.

### Time Complexity

```
O(n²)
```

for all cases.

---

# Insertion Sort Implementation

Insertion Sort inserts each new element into its correct position within the already sorted prefix.

The same three datasets are used.

### Results

| Input Order | Approximate Time |
|--------------|-----------------|
| Random | ~2 s |
| Ascending | Very small (almost instantaneous) |
| Descending | ~5 s |

### Observation

Insertion Sort is highly dependent on the initial order.

#### Best Case

Already sorted list.

Each element is already in the correct position.

```
O(n)
```

#### Worst Case

Reverse sorted list.

Every new element must be shifted to the beginning.

```
O(n²)
```

---

# Recursive Insertion Sort

Insertion Sort is also implemented recursively.

### Problem

Python limits the recursion depth to approximately **1000** function calls.

Sorting larger lists causes a recursion depth error.

### Solution

Increase the recursion limit using:

```python
import sys
sys.setrecursionlimit(2**31 - 1)
```

---

## Performance

Even after increasing the recursion limit, recursive insertion sort is much slower.

Example:

- Recursive Insertion Sort on **2000** elements takes approximately **12 seconds**.

The iterative version sorts much larger inputs considerably faster.

### Reason

Recursive function calls introduce additional overhead:

- Function creation
- Parameter passing
- Stack management
- Returning from recursive calls

Although both versions have the same asymptotic complexity, recursion increases the constant factors significantly.

---

# Merge Sort Implementation

Merge Sort is implemented using two functions:

- **merge()**
- **mergeSort()**

The merge function combines two sorted lists into one sorted list.

---

## Correctness Test

Example input:

```
0,2,4,6,...
followed by
1,3,5,7,...
```

After Merge Sort:

```
0,1,2,3,4,5,6,7,...
```

This verifies that the implementation is correct.

---

# Performance of Merge Sort

### Experiment

Input size:

```
10⁶ elements
```

Three types of inputs are tested:

- Random
- Ascending
- Descending

### Results

| Input Order | Approximate Time |
|--------------|-----------------|
| Random | < 10 seconds |
| Ascending | ~5 seconds |
| Descending | ~5 seconds |

### Observation

Merge Sort efficiently handles very large datasets.

Its running time remains close to the theoretical prediction.

### Time Complexity

```
O(n log n)
```

---

# Comparison of Algorithms

| Algorithm | Best Case | Worst Case | Depends on Input? |
|------------|-----------|------------|-------------------|
| Linear Search | O(1) | O(n) | Yes |
| Binary Search | O(1) | O(log n) | Requires sorted list |
| Selection Sort | O(n²) | O(n²) | No |
| Insertion Sort | O(n) | O(n²) | Yes |
| Merge Sort | O(n log n) | O(n log n) | Very little |

---

# Key Observations

- Binary Search is much faster than Linear Search on sorted data.
- Selection Sort performs almost the same regardless of input order.
- Insertion Sort is extremely efficient for nearly sorted data but performs poorly on reverse-sorted data.
- Recursive implementations incur additional overhead compared to iterative implementations.
- Merge Sort efficiently handles very large datasets due to its **O(n log n)** complexity.
- Experimental results closely match the theoretical time complexity derived in previous lectures.
```