# Lecture 07: Implementation of Lists in Python

> **Course:** Programming, Data Structures and Algorithms using Python
>
> **Week:** 3
>
> **Lecture:** 7

---

# Lecture Notes

## Overview

In the previous lecture, we learned how flexible linked lists can be implemented using nodes. This lecture explains how **Python actually implements its built-in lists** and compares them with classical linked lists and arrays.

Although Python provides a data structure called a *list*, it is **not implemented as a linked list**. Instead, Python lists are implemented internally using **dynamic arrays**, allowing fast indexing while still supporting flexible resizing.

The lecture also introduces the **NumPy** library, which provides true multidimensional arrays and efficient mathematical operations.

---

## Review: Lists vs Arrays

Two common ways of storing sequences are:

- Linked Lists
- Arrays

### Linked Lists

A linked list is a flexible structure.

Characteristics:

- Can grow or shrink easily.
- Insertions and deletions are efficient.
- Elements are scattered throughout memory.
- Accessing the ith element requires traversing the list.

Time complexity:

```
Access ith element = O(n)

Insertion (known position) = O(1)

Deletion (known position) = O(1)
```

---

### Arrays

Arrays occupy one continuous block of memory.

Characteristics:

- Fixed size.
- Support random access.
- Elements are stored contiguously.
- Insertion or deletion requires shifting elements.

Time complexity:

```
Access ith element = O(1)

Insertion = O(n)

Deletion = O(n)
```

---

## Are Python Lists Actually Linked Lists?

Surprisingly,

**No.**

Python lists are **implemented internally as dynamic arrays**, not linked lists.

When a Python list is created,

Python allocates a contiguous block of memory that is **larger than the current number of elements**.

For example,

```
Allocated Array

+----+----+----+----+----+----+----+----+

| 10 | 20 | 30 |    |    |    |    |    |

+----+----+----+----+----+----+----+----+

                 ↑

          First free location
```

The extra unused space allows the list to grow without reallocating memory after every insertion.

---

## Growing a Python List

Suppose we append another element.

Before:

```
10 20 30
```

After:

```
10 20 30 40
```

Python simply stores the new element in the next free position.

```
Append

Before

10 20 30 _ _ _

After

10 20 30 40 _ _
```

Since no shifting is required,

```
append()

Time Complexity = O(1)
```

for most operations.

---

## The pop() Operation

Python also provides

```
pop()
```

which removes the last element.

Example:

Before

```
10 20 30 40
```

After

```
10 20 30
```

Python only moves the pointer marking the end of the list.

No elements need to be shifted.

Therefore,

```
pop()

Time Complexity = O(1)
```

---

## What Happens When the Array Becomes Full?

Eventually,

all allocated positions become occupied.

Example:

```
10 20 30 40 50 60
```

No free space remains.

Python then allocates a **new array of approximately double the previous size**.

```
Old Array

+----+----+----+----+

10   20   30   40

↓

New Array

+----+----+----+----+----+----+----+----+

10   20   30   40
```

All existing elements are copied into the larger array.

This copying requires

```
O(n)
```

time.

---

## Why append() Is Still Considered O(1)

Although resizing requires O(n) time,

it happens only occasionally.

Suppose:

- n append operations each take O(1)
- one resize operation takes O(n)

Total work:

```
n + n = 2n
```

Average work per append:

```
2n / n = 2
```

which is still a constant.

This is called **amortized analysis**.

Therefore,

```
append()

Amortized Complexity = O(1)
```

---

## Insertion and Deletion in the Middle

Appending is fast because new elements are added at the end.

However,

suppose we insert an element in the middle.

```
Before

10 20 30 40

Insert 25

↓

10 20 25 30 40
```

Everything after the insertion point must shift one position to the right.

Similarly,

deleting an element requires shifting all later elements left.

Therefore,

```
insert()

Time Complexity = O(n)
```

and

```
delete()

Time Complexity = O(n)
```

---

## Conclusion About Python Lists

Despite their name,

Python lists behave much more like **dynamic arrays** than linked lists.

Summary of important operations:

| Operation | Complexity |
|------------|------------|
| Indexing | O(1) |
| Append | O(1) amortized |
| Pop (last element) | O(1) |
| Insert in middle | O(n) |
| Delete in middle | O(n) |

---

# Key Takeaways

- Python lists are implemented as **dynamic arrays**, not linked lists.
- Python allocates extra memory so lists can grow efficiently.
- `append()` adds elements at the end and has **amortized O(1)** complexity.
- `pop()` removes the last element in **O(1)** time.
- When the allocated array becomes full, Python creates a **new array of approximately double the size** and copies all elements.
- Although resizing requires **O(n)** time, it happens infrequently, so the average cost per append remains **O(1)**.
- Inserting or deleting elements in the middle requires shifting elements, giving **O(n)** complexity.
- Python lists provide the convenience of flexible resizing while retaining the fast indexing advantages of arrays.
- Python lists are ideal for general-purpose programming, but for numerical computations and multidimensional arrays, **NumPy arrays** are more suitable.

---

# Summary

Although Python calls its primary sequence data structure a **list**, it is actually implemented as a **dynamic array**. Python allocates extra memory to allow efficient growth, making operations like `append()` and `pop()` very fast on average. When the allocated space is exhausted, Python creates a larger array and copies the existing elements, an operation analyzed using **amortized complexity**, which keeps the average append cost at **O(1)**. However, inserting or deleting elements in the middle remains expensive because all subsequent elements must be shifted. The lecture also introduces **NumPy arrays**, which provide true multidimensional arrays and support efficient mathematical and matrix operations, making them the preferred choice for scientific computing.

---

# Flashcards

### Flashcard 1

**Q:** Are Python lists implemented as linked lists?

**A:** No. Python lists are implemented as dynamic arrays.

---

### Flashcard 2

**Q:** Why does Python allocate extra memory for lists?

**A:** To allow efficient growth without reallocating memory after every append.

---

### Flashcard 3

**Q:** What is the time complexity of accessing an element by index in a Python list?

**A:** O(1)

---

### Flashcard 4

**Q:** What is the amortized time complexity of `append()`?

**A:** O(1)

---

### Flashcard 5

**Q:** Why is `append()` considered amortized O(1) instead of always O(1)?

**A:** Because resizing occasionally requires copying all elements into a larger array, but this cost is spread over many append operations.

---

### Flashcard 6

**Q:** What happens when a Python list becomes full?

**A:** Python allocates a larger array (typically about twice the size) and copies all existing elements into it.

---

### Flashcard 7

**Q:** What is the time complexity of inserting an element in the middle of a Python list?

**A:** O(n)

---

### Flashcard 8

**Q:** Why is insertion in the middle expensive?

**A:** Because all subsequent elements must be shifted one position to the right.

---

### Flashcard 9

**Q:** What is the time complexity of deleting an element from the middle of a Python list?

**A:** O(n)

---

### Flashcard 10

**Q:** Which library provides true multidimensional arrays in Python?

**A:** NumPy.

---

### Flashcard 11

**Q:** Which NumPy function creates an array filled with zeros?

**A:** `np.zeros()`

---

### Flashcard 12

**Q:** What is wrong with creating a matrix using repeated references like `[[0]*3]*3`?

**A:** All rows refer to the same list, so modifying one row changes every row.

---

### Flashcard 13

**Q:** How can independent rows be created in a Python matrix?

**A:** Using list comprehension.

Example:

```python
matrix = [[0 for j in range(3)] for i in range(3)]
```

---

### Flashcard 14

**Q:** What advantage do NumPy arrays have over nested Python lists?

**A:** They support efficient vectorized and matrix operations without explicit nested loops.

---

### Flashcard 15

**Q:** Which NumPy function converts a Python sequence into an array?

**A:** `np.array()`

---

# Practice Quiz

## Multiple Choice Questions

### Q1.

Python lists are internally implemented as:

A. Linked Lists

B. Trees

C. Dynamic Arrays

D. Hash Tables

**Answer:** C

---

### Q2.

The amortized complexity of `append()` is:

A. O(n)

B. O(log n)

C. O(1)

D. O(n²)

**Answer:** C

---

### Q3.

When a Python list becomes full, Python:

A. Deletes old elements

B. Creates a larger array and copies the elements

C. Converts the list into a linked list

D. Stops accepting new elements

**Answer:** B

---

### Q4.

Which operation on a Python list generally requires shifting elements?

A. `append()`

B. Indexing

C. `insert()`

D. `pop()` from the end

**Answer:** C

---

### Q5.

The time complexity of inserting an element in the middle of a Python list is:

A. O(1)

B. O(log n)

C. O(n)

D. O(n log n)

**Answer:** C

---

### Q6.

Which library provides efficient multidimensional arrays in Python?

A. math

B. random

C. NumPy

D. collections

**Answer:** C

---

### Q7.

Which NumPy function creates an array initialized with zeros?

A. `np.array()`

B. `np.zeros()`

C. `np.range()`

D. `np.matrix()`

**Answer:** B

---

### Q8.

Why should `[[0]*3]*3` generally be avoided for creating matrices?

A. It is slower than NumPy.

B. It creates rows with different lengths.

C. All rows reference the same list.

D. It cannot store integers.

**Answer:** C

---

## Short Answer Questions

### Q1.

Why is `append()` considered amortized O(1) even though resizing takes O(n)?

**Answer:**

Because resizing occurs only occasionally. The O(n) copying cost is spread over many append operations, making the average cost per append constant.

---

### Q2.

Why are insertions in the middle of a Python list expensive?

**Answer:**

Because Python lists are dynamic arrays, inserting an element requires shifting all subsequent elements one position to the right, resulting in O(n) time.

---

### Q3.

Why is NumPy preferred over nested Python lists for numerical computations?

**Answer:**

NumPy provides true multidimensional arrays, efficient memory usage, and optimized vectorized operations such as element-wise arithmetic and matrix multiplication, making numerical computations much faster.