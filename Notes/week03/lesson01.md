# Lesson: Stack and Queue

> **Course:** Programming, Data Structures and Algorithms using Python
>
> **Week:** 3
>
> **Lesson:** 1

---

# Lecture Notes

## Overview

This lesson introduces two fundamental linear data structures used extensively in computer science: **Stack** and **Queue**.

A **Stack** follows the **Last In First Out (LIFO)** principle, where the most recently inserted element is removed first. A **Queue**, on the other hand, follows the **First In First Out (FIFO)** principle, where the earliest inserted element is removed first.

The lesson discusses their definitions, basic operations, common applications, and possible implementations in Python.

---

# Stack

A **Stack** is a **non-primitive linear data structure** in which insertion and deletion are performed from **only one end**, called the **top** of the stack. :contentReference[oaicite:0]{index=0}

Because the last inserted element is the first one removed, a stack follows the **Last In First Out (LIFO)** principle.

### LIFO Principle

```
Push A

A

Push B

B
A

Push C

C
B
A

Pop

B
A
```

The last inserted element (**C**) is removed first.

---

## Basic Operations on Stack

### 1. Push

The **Push** operation inserts a new element onto the **top** of the stack. :contentReference[oaicite:1]{index=1}

Example:

Before

```
Top

30
20
10
```

Push 40

After

```
Top

40
30
20
10
```

---

### 2. Pop

The **Pop** operation removes the element at the **top** of the stack and returns its value. :contentReference[oaicite:2]{index=2}

Example:

Before

```
Top

40
30
20
10
```

Pop

Returns:

```
40
```

Remaining Stack

```
Top

30
20
10
```

---

### 3. Traverse (Display)

Traversal means accessing every element of the stack from **top to bottom**. :contentReference[oaicite:3]{index=3}

Example:

```
Top

50
40
30
20
10
```

Traversal Output

```
50
40
30
20
10
```

---

## Applications of Stack

Stacks are commonly used in many computing applications, including: :contentReference[oaicite:4]{index=4}

- Reversing strings
- Expression evaluation
- Undo/Redo operations
- Backtracking algorithms
- Depth First Search (DFS) in graphs

---

## Implementation of Stack in Python

A stack can be implemented using:

- Python Lists
- Linked Lists :contentReference[oaicite:5]{index=5}

Using a Python list:

```python
stack = []

stack.append(10)
stack.append(20)
stack.append(30)

print(stack)

x = stack.pop()

print(x)
print(stack)
```

Output

```
[10, 20, 30]

30

[10, 20]
```

---

# Queue

A **Queue** is a **non-primitive linear data structure** in which insertion takes place at one end called the **Back (Rear)**, while deletion occurs at the opposite end called the **Front**. :contentReference[oaicite:6]{index=6}

A queue follows the **First In First Out (FIFO)** principle.

---

## FIFO Principle

```
Enqueue A

Front Rear

A

Enqueue B

Front

A B

Rear

Enqueue C

Front

A B C

Rear

Dequeue

Front

B C

Rear
```

The first inserted element (**A**) leaves first.

---

## Basic Operations on Queue

### 1. Enqueue

The **Enqueue** operation inserts a new element at the **Back (Rear)** of the queue. :contentReference[oaicite:7]{index=7}

Example

Before

```
Front

10 20 30

Rear
```

Enqueue 40

After

```
Front

10 20 30 40

Rear
```

---

### 2. Dequeue

The **Dequeue** operation removes and returns the element at the **Front** of the queue. :contentReference[oaicite:8]{index=8}

Example

Before

```
Front

10 20 30 40

Rear
```

Dequeue

Returns

```
10
```

Remaining Queue

```
Front

20 30 40

Rear
```

---

### 3. Traverse (Display)

Traversal means accessing each element from **Front to Back**. :contentReference[oaicite:9]{index=9}

Example

```
Front

5 10 15 20

Rear
```

Traversal Output

```
5
10
15
20
```

---

## Applications of Queue

Queues are commonly used in: :contentReference[oaicite:10]{index=10}

- Printer spooling
- Job scheduling in operating systems
- Waiting list applications
- Breadth First Search (BFS) in graphs

---

## Implementation of Queue in Python

Queues can be implemented using:

- Python Lists
- Linked Lists :contentReference[oaicite:11]{index=11}

Example using a list:

```python
queue = []

queue.append(10)
queue.append(20)
queue.append(30)

print(queue)

x = queue.pop(0)

print(x)
print(queue)
```

Output

```
[10, 20, 30]

10

[20, 30]
```

---

# Key Takeaways

- A **Stack** follows the **Last In First Out (LIFO)** principle.
- In a stack, insertion and deletion occur only at the **top**.
- The primary stack operations are **Push**, **Pop**, and **Traverse**.
- Common stack applications include expression evaluation, undo/redo functionality, string reversal, backtracking, and Depth First Search.
- A **Queue** follows the **First In First Out (FIFO)** principle.
- In a queue, insertion occurs at the **rear**, while deletion occurs at the **front**.
- The primary queue operations are **Enqueue**, **Dequeue**, and **Traverse**.
- Common queue applications include printer scheduling, operating system job scheduling, waiting lists, and Breadth First Search.
- Both stacks and queues can be implemented using Python lists or linked lists.

---

# Summary

Stacks and queues are two fundamental linear data structures with different access policies. A stack follows the Last In First Out (LIFO) principle, allowing insertion and deletion only from the top, making it suitable for tasks such as expression evaluation, undo operations, and depth-first search. A queue follows the First In First Out (FIFO) principle, where elements are inserted at the rear and removed from the front, making it ideal for scheduling, waiting systems, and breadth-first search. Both data structures support three basic operations—insert, delete, and traverse—and can be implemented in Python using either lists or linked lists.

---

# Flashcards

### Flashcard 1

**Q:** What type of data structure is a Stack?

**A:** A non-primitive linear data structure.

---

### Flashcard 2

**Q:** Which principle does a Stack follow?

**A:** Last In First Out (LIFO).

---

### Flashcard 3

**Q:** What operation adds an element to a Stack?

**A:** Push.

---

### Flashcard 4

**Q:** What operation removes the top element of a Stack?

**A:** Pop.

---

### Flashcard 5

**Q:** From which direction is a Stack traversed?

**A:** Top to bottom.

---

### Flashcard 6

**Q:** Name two applications of a Stack.

**A:** Undo/Redo operations and Depth First Search (DFS).

---

### Flashcard 7

**Q:** Which principle does a Queue follow?

**A:** First In First Out (FIFO).

---

### Flashcard 8

**Q:** What operation inserts an element into a Queue?

**A:** Enqueue.

---

### Flashcard 9

**Q:** What operation removes an element from a Queue?

**A:** Dequeue.

---

### Flashcard 10

**Q:** From which end is an element removed in a Queue?

**A:** The Front.

---

### Flashcard 11

**Q:** Name two applications of a Queue.

**A:** Printer spooling and Breadth First Search (BFS).

---

### Flashcard 12

**Q:** Which two data structures can be used to implement both stacks and queues in Python?

**A:** Python lists and linked lists.

---

# Practice Quiz

## Multiple Choice Questions

### Q1.

A Stack follows which principle?

A. FIFO

B. LIFO

C. Random Access

D. Priority

**Answer:** B

---

### Q2.

Which operation removes the top element of a Stack?

A. Push

B. Enqueue

C. Pop

D. Delete

**Answer:** C

---

### Q3.

A Queue follows which principle?

A. LIFO

B. FIFO

C. Random Access

D. Circular Access

**Answer:** B

---

### Q4.

Which Queue operation inserts a new element?

A. Push

B. Pop

C. Enqueue

D. Dequeue

**Answer:** C

---

### Q5.

Which graph traversal algorithm uses a Stack?

A. BFS

B. DFS

C. Dijkstra

D. Prim

**Answer:** B

---

### Q6.

Which graph traversal algorithm uses a Queue?

A. DFS

B. BFS

C. Kruskal

D. Floyd-Warshall

**Answer:** B

---

### Q7.

Which of the following is an application of a Queue?

A. Undo operation

B. Expression evaluation

C. Printer spooling

D. Backtracking

**Answer:** C

---

### Q8.

Which Python data structure can directly implement a Stack?

A. Dictionary

B. Tuple

C. List

D. Set

**Answer:** C

---

## Short Answer Questions

### Q1.

Why is a Stack called a LIFO data structure?

**Answer:**

Because the last element inserted into the stack is the first one removed.

---

### Q2.

How does a Queue differ from a Stack?

**Answer:**

A Queue follows the FIFO principle, where the first inserted element is removed first, whereas a Stack follows the LIFO principle, where the last inserted element is removed first.

---

### Q3.

Name three real-world applications of queues.

**Answer:**

Printer spooling, job scheduling in operating systems, and waiting list or ticketing systems.