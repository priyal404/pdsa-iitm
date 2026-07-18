# Lecture 3: Breadth First Search (BFS)

> **Course:** Programming, Data Structures and Algorithms using Python
>
> **Week:** Graphs
>
> **Lecture:** Breadth First Search (BFS)

---

# Introduction / Overview

Breadth First Search (BFS) is the first systematic graph traversal technique used to solve the **reachability problem**. Starting from a source vertex, BFS explores all vertices that are one edge away, then all vertices two edges away, and so on. This level-wise exploration guarantees that vertices are visited in increasing order of their distance (number of edges) from the source.

Unlike Depth First Search (DFS), which explores one path completely before backtracking, BFS expands uniformly across the graph.

---

# Main Topics

## Revisiting the Reachability Problem

The objective is to determine which vertices can be reached from a given source vertex.

General strategy:

1. Mark the starting vertex as reachable.
2. Visit all its neighbours.
3. Visit neighbours of those neighbours.
4. Continue until no new vertices can be reached.

To avoid infinite loops in cyclic graphs, every visited vertex must be marked so that it is processed only once.

---

## BFS vs DFS

| Breadth First Search | Depth First Search |
|----------------------|--------------------|
| Explores level by level | Explores one path completely |
| Visits nearest vertices first | Goes as deep as possible before backtracking |
| Uses a Queue | Uses a Stack / Recursion |
| Finds shortest path (in terms of edges) in unweighted graphs | Does not necessarily find the shortest path |

---

## Level-wise Exploration

Suppose the source vertex is **S**.

```text
Level 0 : S

Level 1 : All neighbours of S

Level 2 : Neighbours of Level 1

Level 3 : Neighbours of Level 2

...
```

This expansion gives BFS its name—**Breadth First Search**—because the search grows wider before going deeper.

---

## Visiting vs Exploring

BFS distinguishes between two operations.

### Visited

A vertex has been discovered for the first time.

### Explored

All neighbours of that vertex have been examined.

A vertex should be:

- Visited exactly once.
- Explored exactly once.

This prevents repeated work and infinite cycles.

---

## Tracking Visited Vertices

A Boolean array (or dictionary) is maintained.

Initially,

```python
visited[v] = False
```

for every vertex.

Whenever a vertex is first discovered,

```python
visited[v] = True
```

After this, the vertex is never inserted into the traversal again.

---

## Why Do We Need a Queue?

After visiting a vertex, we cannot immediately explore all newly discovered vertices. We must process them in the order in which they were discovered.

A **Queue (FIFO - First In First Out)** naturally supports this behaviour.

```text
Add --> [Queue] --> Remove

First Added
     ↓
First Removed
```

Operations:

- **Enqueue:** Add element at the rear.
- **Dequeue:** Remove element from the front.

---

## Queue Operations

Conceptually,

```python
enqueue(x)
```

adds an element.

```python
dequeue()
```

removes the oldest element.

```python
isEmpty()
```

checks whether processing is complete.

The queue guarantees that vertices discovered earlier are explored earlier.

---

## Queue Example

Initially,

```text
Queue = [ ]
```

Insert

```text
0
```

```text
[0]
```

Insert

```text
1
```

```text
[0,1]
```

Insert

```text
2
```

```text
[0,1,2]
```

Now remove:

```text
Remove → 0

Queue = [1,2]
```

```text
Remove → 1

Queue = [2]
```

```text
Remove → 2

Queue = [ ]
```

This First-In-First-Out behaviour is exactly what BFS requires.

---

## Basic BFS Procedure

Starting from source vertex **v**:

1. Mark **v** as visited.
2. Insert **v** into the queue.
3. While the queue is not empty:
   - Remove the front vertex.
   - Examine all its neighbours.
   - If a neighbour has not been visited:
     - Mark it visited.
     - Insert it into the queue.

Thus every reachable vertex is discovered exactly once.

---

## BFS Algorithm

```python
BFS(G, s)

Mark every vertex as unvisited

visited[s] = True

enqueue(s)

while queue is not empty:

    u = dequeue()

    for every neighbour v of u:

        if not visited[v]:

            visited[v] = True

            enqueue(v)
```

The algorithm terminates when the queue becomes empty.

At this point, every reachable vertex has been visited.

---

## Example Traversal

Suppose BFS starts from vertex **7**.

Initial queue:

```text
[7]
```

Process **7**

```text
Queue

[4,5,8]
```

Process **4**

```text
Queue

[5,8,0,3]
```

Process **5**

```text
Queue

[8,0,3,6]
```

Process **8**

```text
Queue

[0,3,6,9]
```

The process continues until the queue becomes empty.

Vertices are explored strictly in the order they were discovered.

---

## Why Is Each Vertex Processed Only Once?

Whenever a new vertex is discovered,

```python
visited[v] = True
```

is set immediately.

Therefore,

- it can never be inserted into the queue again,
- it can never be explored twice.

This makes BFS efficient even when cycles exist.

---

## Time Complexity

Assume

- **n** vertices
- **m** edges

### Using Adjacency Matrix

Each explored vertex scans an entire row of the matrix.

Each scan takes

```text
O(n)
```

Since there are at most **n** vertices,

| Operation | Complexity |
|-----------|------------|
| Initialization | O(n) |
| Exploration | O(n²) |

Overall,

```text
O(n²)
```

---

## Using Adjacency List

Each vertex still enters the queue only once.

However, only actual neighbours are examined.

Important observation:

The sum of degrees of all vertices equals

```text
2m
```

because every edge contributes to the degree of two vertices.

Therefore,

Total neighbour exploration

```text
O(2m)
```

Overall complexity becomes

```text
O(n + m)
```

which is significantly better for sparse graphs.

---

## Amortized Analysis

Although different vertices may have different numbers of neighbours,

```text
Total work
=
Sum of all vertex degrees
=
2m
```

Instead of analysing each vertex separately, we analyse the total work performed across the entire algorithm.

This is called **amortized analysis**.

For sparse graphs,

```text
O(n+m)
```

is considered the optimal running time for BFS.

---

## Recovering the Path

So far, BFS only tells us **which vertices are reachable**. Often, we also want to know **how to reach a particular vertex**.

To reconstruct the path, BFS maintains another array called **parent**.

### Parent Array

Whenever a vertex `k` is discovered from vertex `j`,

```python
parent[k] = j
```

Thus, every visited vertex (except the source) remembers the vertex from which it was first reached.

Initially,

```python
parent[v] = -1
```

for every vertex.

The source vertex also has parent `-1` because it is not reached from any other vertex.

---

## BFS with Parent Information

```python
BFS(G, s)

Initialize:

visited[v] = False
parent[v] = -1

visited[s] = True

enqueue(s)

while queue is not empty:

    u = dequeue()

    for every neighbour x of u:

        if not visited[x]:

            visited[x] = True

            parent[x] = u

            enqueue(x)

return visited, parent
```

The only addition compared to standard BFS is recording the parent before inserting a newly discovered vertex into the queue.

---

## Reconstructing a Path

Suppose BFS starts from vertex **7**.

During traversal,

```text
parent[4] = 7
parent[0] = 4
parent[1] = 0
```

To find the path from **7** to **1**, trace the parent links backwards.

```text
1 ← 0 ← 4 ← 7
```

Reverse the sequence:

```text
7 → 4 → 0 → 1
```

Similarly,

```text
parent[6] = 5
parent[5] = 7
```

gives

```text
7 → 5 → 6
```

Thus, the parent array allows the actual traversal path to be recovered.

---

## Recording Levels

Since BFS explores the graph level by level, we can also record the **distance (in terms of edges)** from the source.

Instead of using

```python
visited[]
```

we maintain

```python
level[]
```

where

```text
level = -1
```

means **not visited**.

Initially,

```python
level[v] = -1
parent[v] = -1
```

For the source,

```python
level[source] = 0
```

because it is zero edges away from itself.

Whenever a neighbour is discovered,

```python
level[child] = level[parent] + 1
```

Hence, every newly discovered vertex is exactly one level deeper than the vertex from which it was reached.

---

## BFS with Level Array

```python
BFS(G, s)

Initialize:

level[v] = -1
parent[v] = -1

level[s] = 0

enqueue(s)

while queue is not empty:

    u = dequeue()

    for every neighbour x of u:

        if level[x] == -1:

            level[x] = level[u] + 1

            parent[x] = u

            enqueue(x)

return level, parent
```

The `level` array now provides both:

- Whether a vertex was visited (`level != -1`)
- The shortest distance from the source (in number of edges)

---

## Example of Levels

Suppose BFS starts from **7**.

```text
Level 0

7
```

```text
Level 1

4   5   8
```

```text
Level 2

0   3   6   9
```

```text
Level 3

1   2
```

Thus,

| Vertex | Level |
|---------|------:|
| 7 | 0 |
| 4, 5, 8 | 1 |
| 0, 3, 6, 9 | 2 |
| 1, 2 | 3 |

The level value equals the minimum number of edges required to reach that vertex from the source.

---

## Shortest Path Property

Because BFS visits vertices in increasing order of their levels,

- the **first time** a vertex is discovered,
- it has already been reached using the **fewest possible edges**.

Therefore, BFS computes the **shortest path in terms of the number of edges** for **unweighted graphs**.

> **Note:** This does **not** necessarily mean the minimum-cost path if edges have different weights.

---

# Key Takeaways

- BFS explores a graph level by level.
- A queue ensures vertices are processed in FIFO order.
- Every vertex is visited and explored at most once.
- The `visited` array prevents revisiting vertices.
- The `parent` array allows reconstruction of paths.
- The `level` array stores the shortest distance (number of edges) from the source.
- BFS runs in **O(n²)** using an adjacency matrix and **O(n + m)** using an adjacency list.

---

# Important Formulae

### Sum of Degrees

```text
Σ degree(v) = 2m
```

where `m` is the number of edges.

---

### Time Complexity

| Representation | Complexity |
|---------------|------------|
| Adjacency Matrix | O(n²) |
| Adjacency List | O(n + m) |

---

### Level Update

```text
level(child) = level(parent) + 1
```

---

# GATE / Interview Focus

- BFS uses a **Queue (FIFO)**.
- Visits vertices level by level.
- Finds shortest paths only in **unweighted graphs**.
- Parent array reconstructs the actual path.
- Level array gives shortest distance from the source.
- Adjacency List implementation is preferred due to **O(n + m)** complexity.
- Understand why the sum of degrees equals **2m** (basis of amortized analysis).

---

# Common GATE Questions

1. Why does BFS use a queue instead of a stack?
2. Explain the difference between **visited**, **parent**, and **level** arrays.
3. Why does BFS guarantee the shortest path in an unweighted graph?
4. Compare BFS using adjacency matrix and adjacency list.
5. Explain amortized analysis for BFS.
6. Why is the sum of all vertex degrees equal to `2m`?
7. What is the time complexity of BFS for sparse graphs?

---

# Flashcards

**Q:** Which data structure is used in BFS?

**A:** Queue (FIFO).

---

**Q:** Why is the `visited` array required?

**A:** To ensure each vertex is processed only once.

---

**Q:** What does the `parent` array store?

**A:** The vertex from which a node was first discovered.

---

**Q:** What does the `level` array represent?

**A:** The minimum number of edges from the source.

---

**Q:** Which graph representation gives BFS complexity `O(n + m)`?

**A:** Adjacency List.

---

**Q:** Why is the sum of all vertex degrees `2m`?

**A:** Every edge contributes to the degree of both its endpoints.

---

# Practice MCQs

### Q1.

Which data structure is fundamental to BFS?

A. Stack

B. Queue

C. Heap

D. Tree

**Answer:** B

---

### Q2.

BFS explores vertices

A. Randomly

B. By increasing edge weights

C. Level by level

D. Using recursion

**Answer:** C

---

### Q3.

The parent array is used to

A. Detect cycles

B. Compute graph colouring

C. Reconstruct paths

D. Count edges

**Answer:** C

---

### Q4.

The time complexity of BFS using an adjacency list is

A. O(n²)

B. O(log n)

C. O(n + m)

D. O(m²)

**Answer:** C

---

### Q5.

In BFS, the level of a newly discovered neighbour is

A. Same as the current vertex

B. One less than the current vertex

C. One more than the current vertex

D. Equal to its degree

**Answer:** C

---

# One-Page Revision

## Breadth First Search

- Explores vertices **level by level**.
- Uses a **Queue (FIFO)**.
- Visits every reachable vertex exactly once.

---

### Arrays Used

| Array | Purpose |
|--------|---------|
| `visited` | Prevent revisiting |
| `parent` | Reconstruct path |
| `level` | Store shortest distance |

---

### Complexity

| Representation | Time |
|---------------|------|
| Adjacency Matrix | **O(n²)** |
| Adjacency List | **O(n + m)** |

---