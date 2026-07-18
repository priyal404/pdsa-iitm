# Lecture 06: Designing a Flexible List and Operations on the Same

> **Course:** Programming, Data Structures and Algorithms using Python
>
> **Week:** 3
>
> **Lecture:** 6

---

# Lecture Notes

## Overview

In the previous lecture, we studied the theoretical differences between **lists** and **arrays**. This lecture focuses on **how a flexible list (linked list) can actually be implemented in Python**.

A linked list is represented as a sequence of **nodes**, where each node stores:

- A value
- A reference (pointer) to the next node

The lecture introduces the basic node structure, representation of an empty list, and discusses operations such as appending and inserting elements.

---

## Structure of a Linked List

A linked list consists of interconnected nodes.

Each node stores:

- The actual data
- A pointer to the next node

Conceptually,

```
Head

↓

+-------+-------+
| Value | Next |
+-------+-------+

          ↓

+-------+-------+
| Value | Next |
+-------+-------+

          ↓

       NULL
```

The last node points to:

```
None
```

---

## Designing a Node Class

Each node can be represented using a Python class.

A node contains two attributes:

- `value`
- `next`

Pseudo-implementation:

```python
class Node:

    def __init__(self, v=None):
        self.value = v
        self.next = None
```

Here,

- `self.value` stores the data.
- `self.next` stores a reference to the next node.
- Initially, the next reference is `None`.

---

## Understanding `self`

In Python classes,

```
self
```

refers to the current object.

Therefore,

```
self.value
```

means

> the value stored in the current node.

Similarly,

```
self.next
```

refers to the next node connected to the current node.

---

## Representing an Empty List

Unlike many programming languages, Python does not require explicit variable type declarations.

For example,

```python
l = []
```

creates an empty Python list.

However, when implementing our own linked list, we need a way to represent an empty list.

The convention used in this lecture is:

```
value = None

next = None
```

A node with both fields set to `None` represents an empty list.

Diagram:

```
+-------+-------+
| None  | None |
+-------+-------+
```

---

## Checking Whether a List is Empty

A helper function can determine whether the list is empty.

Pseudo-code:

```python
def isempty(self):

    if self.value is None:
        return True

    return False
```

Observation:

If

```
self.value == None
```

then the list is treated as empty.

The `next` field is not checked because an empty list should never contain additional nodes.

---

## Creating Nodes

Creating an empty node:

```python
l1 = Node()
```

Produces:

```
None
```

Creating a node with data:

```python
l2 = Node(5)
```

Produces:

```
5
```

Checking:

```python
l1.isempty()

True

l2.isempty()

False
```

---

## Building a Linked List

Once nodes are created, they can be connected.

Example:

```
10 → 20 → 30 → None
```

Internally,

```
Node1.next → Node2

Node2.next → Node3

Node3.next → None
```

The variable storing the list points only to the first node.

```
Head

↓

10 → 20 → 30
```

---

## Growing a Linked List

Since linked lists are dynamic,

new nodes can be added without moving existing nodes.

Two common operations are:

- Append
- Insert

---

## Append Operation

Append means inserting a new node at the end of the list.

Example:

Before:

```
10 → 20 → 30
```

Append:

```
40
```

After:

```
10 → 20 → 30 → 40
```

To perform append,

the last node is located,

and its `next` pointer is updated to point to the new node.

---

## Insert Operation

Insert means placing a new node somewhere within the list.

Example:

Before:

```
10 → 30
```

Insert:

```
20
```

After:

```
10 → 20 → 30
```

Only local pointer changes are required.

---

## Why Append is Easier

The lecture notes that append is generally easier than insertion.

Reason:

- Append always occurs at one fixed location (the end).
- Insertion may occur anywhere and requires identifying the correct position first.

---

## Linked List Traversal

To reach any node,

the list must be traversed from the beginning.

Example:

```
Head

↓

10 → 20 → 30 → 40
```

To reach

```
40
```

we must first visit:

```
10

↓

20

↓

30

↓

40
```

Thus,

access remains sequential.

---

## Advantages of This Design

- Dynamic size
- Easy expansion
- Easy contraction
- Efficient pointer updates
- No contiguous memory required

---

## Limitations

- No direct random access
- Sequential traversal required
- Access time increases with list size

---

# Key Takeaways

- A linked list is built using interconnected nodes.
- Each node stores a value and a reference to the next node.
- `self.value` stores data, while `self.next` stores the next node reference.
- An empty list is represented using `value = None` and `next = None`.
- The `isempty()` function checks whether a node represents an empty list.
- Linked lists grow dynamically by linking new nodes.
- Append adds an element at the end of the list.
- Insert adds an element at any desired position.
- Traversal always begins from the head node.
- Linked lists trade faster insertion for slower sequential access.

---

# Summary

This lecture introduces the implementation of flexible lists using linked nodes. Each node contains a value and a reference to the next node, allowing the list to grow or shrink dynamically without requiring contiguous memory. The lecture explains how empty lists are represented, how nodes are created, and how linked lists are extended through append and insert operations. Although linked lists provide excellent flexibility, every operation requiring access to a specific position still requires sequential traversal from the head node.

---

# Flashcards

### Flashcard 1

**Q:** What are the two fields stored in every linked list node?

**A:** A value and a reference (`next`) to the next node.

---

### Flashcard 2

**Q:** What does `self` represent in a Python class?

**A:** The current object (current node).

---

### Flashcard 3

**Q:** How is an empty linked list represented in this implementation?

**A:** A node whose `value` and `next` are both `None`.

---

### Flashcard 4

**Q:** What does the `isempty()` function check?

**A:** Whether `self.value` is `None`.

---

### Flashcard 5

**Q:** What is stored in `self.next`?

**A:** A reference to the next node.

---

### Flashcard 6

**Q:** What does the append operation do?

**A:** Adds a new node at the end of the linked list.

---

### Flashcard 7

**Q:** Why is append generally easier than insert?

**A:** Because append always occurs at the end, while insert may require finding an arbitrary position.

---

### Flashcard 8

**Q:** Why can't linked lists provide random access?

**A:** Because nodes are scattered in memory and must be reached by sequential traversal.

---

### Flashcard 9

**Q:** What does the head of a linked list store?

**A:** A reference to the first node.

---

### Flashcard 10

**Q:** What is the initial value of `next` for a newly created node?

**A:** `None`.

---

# Practice Quiz

## Multiple Choice Questions

### Q1.

Each linked list node stores:

A. Only a value

B. Only a pointer

C. A value and a pointer to the next node

D. Two values

**Answer:** C

---

### Q2.

In this implementation, an empty list is identified by:

A. `next == None`

B. `value == None`

C. `value == 0`

D. `next == 0`

**Answer:** B

---

### Q3.

What does `self.next` represent?

A. Previous node

B. Current node

C. Next node

D. Head node

**Answer:** C

---

### Q4.

Which operation always adds an element at the end of the list?

A. Insert

B. Append

C. Delete

D. Search

**Answer:** B

---

### Q5.

To access the last node of a linked list, we must:

A. Use random access

B. Traverse from the head

C. Use binary search

D. Jump directly using indexing

**Answer:** B

---

## Short Answer Questions

### Q1.

Why is `value = None` used to represent an empty linked list?

**Answer:**
Python does not require explicit type declarations. Using `value = None` provides a simple convention to indicate that the node does not store any valid data and therefore represents an empty list.

---

### Q2.

Why does accessing an arbitrary node in a linked list take linear time?

**Answer:**
Because linked list nodes are connected through pointers rather than stored contiguously. To reach a particular node, traversal must begin from the head and follow each `next` reference until the desired node is reached.