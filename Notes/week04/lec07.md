# Lecture 07: Topological Sorting

> **Course:** Programming Data Structures and Algorithms using Python
>
> **Week:** 4
>
> **Lecture:** 7

---

# Introduction / Overview

In the previous lecture, we learned that **Directed Acyclic Graphs (DAGs)** naturally represent **tasks and their dependencies**.

This lecture introduces one of the most important operations on DAGs:

> **Topological Sorting**

A topological ordering provides a **valid sequence of execution** such that every task is performed **only after all of its prerequisite tasks have been completed**.

Topological sorting is widely used in:

- Course prerequisite scheduling
- Project planning
- Software package installation
- Build systems
- Task scheduling
- Dependency resolution

---

# What is Topological Sorting?

A **Topological Sort** is an ordering of the vertices of a DAG such that:

For every directed edge

```
u → v
```

vertex **u appears before v** in the ordering.

In other words,

**every dependency is satisfied before the dependent task is executed.**

---

## Example

Consider the following graph.

```text
0 ──► 3
      ▲
1 ────┘

3 ──► 5
```

Valid topological orderings include:

```
0 1 3 5
```

or

```
1 0 3 5
```

Both satisfy the dependency:

```
0 before 3
1 before 3
3 before 5
```

---

# Why Cycles Make Topological Sorting Impossible

Suppose we have:

```text
A → B
↑   ↓
└── C
```

The dependencies become

- A before B
- B before C
- C before A

This is impossible because:

```
A must occur before itself.
```

Therefore,

> **A directed graph containing a cycle cannot be topologically sorted.**

Only **Directed Acyclic Graphs (DAGs)** admit a topological ordering.

---

# Fundamental Idea Behind the Algorithm

When scheduling tasks,

the first task executed should have **no prerequisites**.

In graph terminology:

> Start with a vertex having **indegree = 0**

After completing that task,

- remove it from the graph
- remove all outgoing edges

This may create new vertices with indegree 0.

Repeat until every vertex has been processed.

---

# Indegree

The **indegree** of a vertex is the number of incoming edges.

Example:

```text
A → C ← B
```

Indegree table:

| Vertex | Indegree |
|---------|---------:|
| A | 0 |
| B | 0 |
| C | 2 |

Only A and B are immediately executable.

---

# Why Every DAG Has an Indegree-0 Vertex

This fact is the foundation of topological sorting.

## Proof (Idea)

Assume **every vertex has indegree ≥ 1.**

Start from any vertex.

Move backwards along an incoming edge.

Since every vertex has an incoming edge,

you can keep moving backwards forever.

However,

the graph contains only **n vertices**.

Eventually,

a previously visited vertex must be reached.

This forms a **cycle**.

But a DAG contains **no cycles**.

Therefore,

our assumption is false.

Hence,

> **Every DAG has at least one vertex with indegree 0.**

---

# Why the Algorithm Never Gets Stuck

Suppose we remove one indegree-0 vertex.

The graph becomes smaller.

Removing vertices and edges **cannot create a cycle**.

Therefore,

the remaining graph is **still a DAG**.

Since every DAG has an indegree-0 vertex,

we can continue until every vertex has been processed.

Thus,

topological sorting always succeeds for a DAG.

---

# Topological Sorting Algorithm

The algorithm repeatedly performs the following steps:

1. Compute indegree of every vertex.
2. Find a vertex whose indegree is 0.
3. Output that vertex.
4. Remove the vertex and all outgoing edges.
5. Update indegrees.
6. Repeat until all vertices are processed.

---

## Algorithm Flow

```text
Compute Indegrees
        │
        ▼
Find Indegree 0 Vertex
        │
        ▼
Output Vertex
        │
        ▼
Remove Outgoing Edges
        │
        ▼
Update Indegrees
        │
        ▼
Repeat
```

---

# Example

Initial graph:

```text
0 → 2
0 → 3

1 → 2
1 → 7

2 → 5
3 → 5
4 → 7

5 → 6
6 → 7
```

Initial indegrees:

| Vertex | Indegree |
|---------|---------:|
|0|0|
|1|0|
|2|2|
|3|1|
|4|0|
|5|2|
|6|1|
|7|3|

Possible first choices:

```
0
1
4
```

Suppose we choose:

```
1
```

Remove outgoing edges:

```
1 → 2
1 → 7
```

Updated indegrees:

```
2 : 1
7 : 2
```

Now vertex 0 still has indegree 0.

Choose 0.

After removing its edges,

vertex 2 becomes indegree 0.

Continue similarly until all vertices are processed.

One possible ordering is:

```
1 0 3 2 5 6 4 7
```

Another valid ordering could be:

```
0 1 2 3 4 5 6 7
```

Both satisfy all dependencies.

---

# Topological Ordering is NOT Unique

At several stages,

multiple vertices may simultaneously have indegree 0.

Example:

```text
A      B
 \    /
   C
```

Possible orderings:

```
A B C
```

or

```
B A C
```

Both are correct.

Hence,

> **A DAG can have multiple valid topological orderings.**

---

# Python Implementation (Adjacency Matrix)

The lecture first presents an implementation using an **adjacency matrix**.

## Main Steps

1. Compute indegrees by scanning every column.
2. Find a vertex with indegree 0.
3. Append it to the answer.
4. Update indegrees of all outgoing neighbours.
5. Repeat for all vertices.

Pseudo-code:

```python
Compute indegrees

for every vertex:
    find indegree 0 vertex
    add it to answer

    for every neighbour:
        decrease indegree
```

---

## Computing Indegree (Adjacency Matrix)

For each column,

count incoming edges.

```text
0 1 0 0
0 0 1 0
1 0 0 1
```

Column sums give indegrees.

---

## Complexity Analysis

### Computing Indegrees

Need to scan every cell.

```
O(n²)
```

### Main Loop

For each vertex:

- search indegree 0 vertex → O(n)
- update neighbours → O(n)

Overall:

```
O(n²)
```

---

# Improving Using an Adjacency List

The lecture then improves the algorithm using an **adjacency list**.

Instead of repeatedly searching for indegree-0 vertices,

maintain them in a **queue**.

Whenever a vertex becomes indegree 0,

enqueue it immediately.

---

## Improved Algorithm

1. Compute indegrees.
2. Insert all indegree-0 vertices into a queue.
3. Remove front of queue.
4. Output it.
5. Reduce indegrees of neighbours.
6. If neighbour becomes indegree 0,
   enqueue it.
7. Continue until queue is empty.

---

## Queue-Based Illustration

```text
Queue

[0,1]

Remove 0

↓

Update neighbours

↓

Vertex 3 becomes indegree 0

Queue

[1,3]

↓

Remove 1

↓

Continue...
```

---

# Python Implementation (Adjacency List)

Pseudo-code:

```python
Compute indegrees

Queue ← all indegree 0 vertices

while Queue is not empty:

    remove front vertex

    output vertex

    for every neighbour:

        indegree--

        if indegree becomes 0:

            enqueue neighbour
```

This avoids repeatedly scanning all vertices.

---

# Complexity Analysis

Let

- **n** = number of vertices
- **m** = number of edges

## Step 1

Initialize indegrees

```
O(n)
```

Process every edge once

```
O(m)
```

Total

```
O(m+n)
```

---

## Step 2

Each vertex enters the queue once.

```
O(n)
```

---

## Step 3

Each edge is processed exactly once while updating indegrees.

```
O(m)
```

---

## Final Complexity

| Representation | Time Complexity |
|---------------|-----------------|
| Adjacency Matrix | **O(n²)** |
| Adjacency List | **O(m+n)** |

The adjacency-list implementation is much more efficient for sparse graphs.

---

# Comparison: Matrix vs Adjacency List

| Feature | Adjacency Matrix | Adjacency List |
|----------|------------------|----------------|
| Storage | O(n²) | O(m+n) |
| Indegree computation | O(n²) | O(m+n) |
| Finding next vertex | Scan vertices | Queue |
| Overall complexity | O(n²) | O(m+n) |

---

# Applications of Topological Sorting

Topological sorting is useful wherever **dependency constraints** exist.

Examples:

- Course prerequisite planning
- Build dependency resolution
- Package installation
- Project scheduling
- Task execution order
- Workflow management
- Compilation order in software projects

---

# Key Takeaways

- Topological sorting exists **only for DAGs**.
- Every DAG has at least one **indegree-0 vertex**.
- Removing an indegree-0 vertex leaves another DAG.
- The algorithm repeatedly removes indegree-0 vertices.
- Multiple valid topological orders may exist.
- Adjacency matrix implementation takes **O(n²)** time.
- Using an adjacency list and queue improves complexity to **O(m+n)**.

---

# Important Formulae

### Indegree

\[
\text{Indegree}(v)=\text{Number of incoming edges to }v
\]

---

### Time Complexity

Adjacency Matrix:

\[
O(n^2)
\]

Adjacency List:

\[
O(m+n)
\]

where

- \(n\) = number of vertices
- \(m\) = number of edges

---

# GATE / Interview Focus

## Must Remember

- Topological sorting is possible **only if the graph is acyclic**.
- Every DAG has **at least one indegree-0 vertex**.
- Topological ordering is generally **not unique**.
- Queue-based implementation corresponds to **Kahn's Algorithm**.
- Matrix implementation: **O(n²)**
- Adjacency-list implementation: **O(m+n)**.
- If all vertices cannot be processed, the graph contains a cycle.

---

# Common GATE Questions

### Q1. Can a graph with a directed cycle be topologically sorted?

**Answer:** No. A cycle creates circular dependencies, making a valid ordering impossible.

---

### Q2. Why must every DAG contain a vertex with indegree 0?

**Answer:** Otherwise, following incoming edges indefinitely would eventually revisit a vertex, forming a cycle.

---

### Q3. Why is a queue used in Kahn's Algorithm?

**Answer:** It efficiently stores all vertices whose indegree becomes 0, avoiding repeated scans of all vertices.

---

### Q4. Why can multiple topological orderings exist?

**Answer:** Because more than one vertex may simultaneously have indegree 0, allowing different valid choices.

---

# Flashcards

**Q:** What is a topological sort?

**A:** An ordering of vertices where every directed edge goes from an earlier vertex to a later vertex.

---

**Q:** Which graphs can be topologically sorted?

**A:** Directed Acyclic Graphs (DAGs).

---

**Q:** What is indegree?

**A:** The number of incoming edges to a vertex.

---

**Q:** Which algorithm performs queue-based topological sorting?

**A:** Kahn's Algorithm.

---

**Q:** Time complexity using an adjacency list?

**A:** **O(m+n)**.

---

# Practice MCQs

### Q1. Which graph can always be topologically sorted?

A. Undirected graph

B. Directed cyclic graph

C. Directed acyclic graph

D. Complete graph

**Answer:** C

---

### Q2. What is the first vertex selected in topological sorting?

A. Maximum outdegree

B. Minimum outdegree

C. Indegree 0

D. Highest degree

**Answer:** C

---

### Q3. Which data structure improves topological sorting to **O(m+n)**?

A. Stack

B. Heap

C. Queue

D. Linked List

**Answer:** C

---

### Q4. If multiple vertices have indegree 0 simultaneously, then:

A. The graph contains a cycle.

B. The ordering is invalid.

C. Multiple topological orders may exist.

D. The algorithm fails.

**Answer:** C

---

# One-Page Revision

- Topological sorting applies **only to DAGs**.
- Order must satisfy every dependency **u → v ⇒ u before v**.
- Start with **indegree = 0** vertices.
- Remove processed vertex and update neighbours' indegrees.
- Removing a vertex from a DAG leaves another DAG.
- Every edge is processed exactly once in the adjacency-list implementation.
- **Adjacency Matrix:** O(n²)
- **Adjacency List (Kahn's Algorithm):** O(m+n)
- Multiple valid topological orderings may exist.
- Failure to process all vertices indicates the presence of a cycle.