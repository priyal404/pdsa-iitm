# Lecture 08: Longest Path in Directed Acyclic Graphs (DAGs)

> **Course:** Programming Data Structures and Algorithms using Python
>
> **Week:** 2
>
> **Lecture:** 8

---

# Introduction / Overview

In the previous lecture, we studied **Topological Sorting**, which provides a valid order of executing tasks in a **Directed Acyclic Graph (DAG)**.

This lecture builds upon that idea to solve another important problem:

> **Given a DAG, what is the longest path to every vertex?**

The longest path helps determine the **minimum completion time** for tasks that have dependencies.

Unlike general graphs, where finding the longest path is computationally difficult, DAGs allow an efficient solution by processing vertices in **topological order**.

Typical applications include:

- Course prerequisite planning
- Project scheduling
- Construction planning
- Workflow management
- Critical path analysis

---

# Motivation: Course Prerequisites

Suppose each vertex represents a course and every directed edge represents a prerequisite.

Each course requires **one semester**.

Example:

```text
Semester 1:
0      1

Semester 2:
2      3      4

Semester 3:
5

Semester 4:
6

Semester 5:
7
```

Even if multiple courses can be taken simultaneously,

the prerequisite constraints force the program to take **5 semesters**.

The reason is that some courses lie on a dependency chain that cannot be shortened.

---

# Longest Path in a DAG

The **longest path to a vertex** is the maximum number of edges that must be traversed from a starting vertex (one with no prerequisites) to reach that vertex.

It represents the **maximum number of sequential dependencies** before a task can begin.

For scheduling problems:

- Longest path = earliest possible completion stage
- Maximum longest path in the graph = minimum total completion time

---

# Relationship with Topological Sorting

Topological sorting guarantees:

For every edge

```text
u → v
```

vertex **u** is processed before **v**.

Therefore,

when processing a vertex,

all information about its predecessors has already been computed.

This makes topological ordering the ideal framework for computing longest paths.

---

# Recursive Definition of Longest Path

## Case 1: Vertex with Indegree 0

If a vertex has no incoming edges,

it has no prerequisites.

Therefore,

```text
LongestPath(v) = 0
```

Such vertices can be executed immediately.

---

## Case 2: Vertex with Incoming Edges

Suppose

```text
A
 \
  \
   ► C
  /
 /
B
```

To compute the longest path to **C**,

we first determine the longest paths to **A** and **B**.

Then,

```text
LongestPath(C)

=

1 + max(
    LongestPath(A),
    LongestPath(B)
)
```

In words,

> A task must wait for its **latest prerequisite** to finish.

---

# Dynamic Programming Idea

The computation follows an inductive (dynamic programming) approach.

Since every predecessor is processed before the current vertex,

their longest paths are already known.

Thus,

for every edge

```text
u → v
```

we update

```text
LongestPath(v)

=

max(
    LongestPath(v),
    LongestPath(u)+1
)
```

Each vertex is computed only once.

---

# Computing Longest Path During Topological Sort

A key observation from the lecture is:

> We do **not** need to perform topological sorting first and then compute longest paths.

Instead,

both can be computed **simultaneously** in a single traversal.

During topological sorting,

whenever a vertex is removed,

its longest path value is propagated to all of its outgoing neighbours.

---

# Example

Consider the DAG:

```text
0 → 2
0 → 3

1 → 2
1 → 7

2 → 5
3 → 5

5 → 6

4 → 7
6 → 7
```

---

## Step 1

Vertices with indegree 0:

```
0
1
4
```

Initialize:

| Vertex | Longest Path |
|---------|-------------:|
|0|0|
|1|0|
|2|0|
|3|0|
|4|0|
|5|0|
|6|0|
|7|0|

---

## Step 2

Process vertex **1**

Outgoing edges:

```text
1 → 2
1 → 7
```

Update:

```
LP(2)=1

LP(7)=1
```

---

## Step 3

Process vertex **0**

Outgoing edges:

```text
0 → 2
0 → 3
```

Updates:

```
LP(2)=max(1,1)=1

LP(3)=1
```

Notice that

```
LP(2)
```

does **not** change,

because both paths have equal length.

---

## Step 4

Process vertex **3**

Outgoing edge:

```text
3 → 5
```

Update:

```
LP(5)=2
```

---

## Step 5

Process vertex **2**

Outgoing edge:

```text
2 → 5
```

Update:

```
LP(5)

=

max(2,2)

=

2
```

Again,

no change occurs because the existing path is already optimal.

---

## Step 6

Process vertex **5**

```text
5 → 6
```

Update:

```
LP(6)=3
```

---

## Step 7

Process vertex **6**

```text
6 → 7
```

Update:

```
LP(7)=4
```

---

## Step 8

Process vertex **4**

```text
4 → 7
```

Possible update:

```
LP(7)

=

max(4,1)

=

4
```

No improvement occurs.

---

## Final Longest Paths

| Vertex | Longest Path |
|---------|-------------:|
|0|0|
|1|0|
|2|1|
|3|1|
|4|0|
|5|2|
|6|3|
|7|4|

Therefore,

the graph requires

```
4 + 1 = 5 stages
```

to complete all tasks.

(The longest path counts **edges**, while the number of stages or semesters counts **vertices**.)

---

# Algorithm

The algorithm closely resembles **Kahn's Topological Sort**.

## Steps

1. Compute indegree of every vertex.
2. Initialize longest path of every vertex to 0.
3. Insert every indegree-0 vertex into a queue.
4. Repeatedly remove a vertex from the queue.
5. Update longest paths of its neighbours.
6. Decrease neighbour indegrees.
7. Insert neighbours whose indegree becomes 0.

---

## Update Rule

For every edge

```text
u → v
```

perform

```text
LongestPath(v)

=

max(
LongestPath(v),
LongestPath(u)+1
)
```

This is the only additional step compared to ordinary topological sorting.

---

# Pseudocode

```python
Compute indegrees

Initialize longest_path[v]=0

Queue ← all indegree 0 vertices

while Queue is not empty:

    u = dequeue()

    for every neighbour v:

        longest_path[v] = max(
            longest_path[v],
            longest_path[u] + 1
        )

        indegree[v] -= 1

        if indegree[v] == 0:

            enqueue(v)

return longest_path
```

---

# Why Does the Algorithm Work?

The correctness follows directly from topological ordering.

When processing a vertex:

- Every predecessor has already been processed.
- Their longest paths are finalized.
- Therefore, taking the maximum over predecessors gives the correct longest path.

Since every edge is examined exactly once,

all longest paths are computed correctly in one traversal.

---

# Complexity Analysis

Let

- **n** = number of vertices
- **m** = number of edges

### Initialization

- Initialize indegrees → **O(n)**
- Initialize longest paths → **O(n)**

---

### Computing Indegrees

Every edge is visited once.

```
O(m)
```

---

### Main Loop

Each vertex is removed from the queue once.

Each edge is processed exactly once.

```
O(m+n)
```

---

## Overall Complexity

| Operation | Complexity |
|-----------|-----------:|
|Initialization|O(n)|
|Indegree computation|O(m)|
|Queue processing|O(m+n)|

Final complexity:

\[
\boxed{O(m+n)}
\]

Thus,

finding the longest path in a DAG is **linear in the size of the graph**.

---

# Why Is This Problem Easy Only for DAGs?

The lecture concludes with an important observation.

The **Longest Path Problem** exists for every graph.

However,

for graphs containing cycles,

the problem becomes extremely difficult.

To define longest paths,

we must avoid revisiting vertices,

otherwise cycles could produce infinitely long paths.

Finding the longest simple path in a general graph is computationally hard.

In contrast,

DAGs contain **no cycles**,

allowing a simple dynamic programming solution using topological ordering.

---

# DAG vs General Graph

| Feature | DAG | General Graph |
|---------|-----|---------------|
|Cycles|No|May exist|
|Topological Order|Exists|Not always possible|
|Longest Path|Efficient|Computationally hard|
|Time Complexity|**O(m+n)**|No efficient general algorithm known|

---

# Applications

The longest path in a DAG is used in:

- Critical Path Method (CPM)
- Project management
- Course scheduling
- Construction planning
- Software dependency analysis
- Manufacturing workflows
- Task scheduling

---

# Key Takeaways

- Longest path measures the maximum sequence of dependencies before a task can begin.
- Vertices with indegree 0 have longest path 0.
- Longest paths are computed using topological order.
- Update rule:

  \[
  LP(v)=\max(LP(v),LP(u)+1)
  \]

  for every edge \(u \rightarrow v\).

- Longest path computation can be performed **simultaneously** with topological sorting.
- Every edge is processed exactly once, giving an **O(m+n)** algorithm.
- The longest path determines the **minimum completion time** for dependency-constrained tasks.
- Unlike DAGs, the longest path problem in general graphs is computationally difficult.

---

# Important Formulae

### Base Case

\[
LP(v)=0
\]

for every vertex with indegree 0.

---

### Recurrence Relation

For every edge

\[
u \rightarrow v
\]

\[
LP(v)=\max(LP(v),LP(u)+1)
\]

---

### Time Complexity

\[
O(m+n)
\]

where

- \(m\) = number of edges
- \(n\) = number of vertices

---

# GATE / Interview Focus

## Must Remember

- Longest path in a DAG is solved using **topological ordering**.
- Vertices with indegree 0 have longest path 0.
- The update rule is based on **dynamic programming**.
- Longest path and topological sorting can be computed together in one traversal.
- Overall complexity is **O(m+n)**.
- Longest path in a general graph is **computationally hard**, but becomes efficient in DAGs because cycles are absent.

---

# Common GATE Questions

### Q1. Why is topological ordering necessary for longest path computation in a DAG?

**Answer:** It guarantees that all predecessors of a vertex have already been processed, so their longest path values are available when computing the current vertex.

---

### Q2. What is the longest path value for a source vertex?

**Answer:** Zero, since it has no prerequisites.

---

### Q3. What update is performed for every edge \(u \rightarrow v\)?

**Answer:**

\[
LP(v)=\max(LP(v),LP(u)+1)
\]

---

### Q4. Why is the longest path problem difficult in general graphs?

**Answer:** Cycles make it impossible to apply topological ordering, and finding the longest simple path is computationally hard.

---

# Flashcards

**Q:** What does the longest path represent in a scheduling problem?

**A:** The maximum number of sequential dependencies before a task can begin.

---

**Q:** Which graph property enables efficient longest path computation?

**A:** The graph is a Directed Acyclic Graph (DAG).

---

**Q:** What is the longest path value of a source vertex?

**A:** 0.

---

**Q:** Which traversal order is used?

**A:** Topological order.

---

**Q:** Time complexity of longest path in a DAG?

**A:** **O(m+n)**.

---

# Practice MCQs

### Q1. The longest path algorithm for DAGs is based on:

A. BFS

B. DFS

C. Topological Sorting

D. Dijkstra's Algorithm

**Answer:** C

---

### Q2. What is the initial longest path value assigned to a source vertex?

A. -1

B. 0

C. 1

D. Infinity

**Answer:** B

---

### Q3. During processing of an edge \(u \rightarrow v\), which update is performed?

A. \(LP(v)=LP(u)\)

B. \(LP(v)=LP(u)-1\)

C. \(LP(v)=\max(LP(v),LP(u)+1)\)

D. \(LP(v)=1\)

**Answer:** C

---

### Q4. The overall complexity of the longest path algorithm on a DAG using an adjacency list is:

A. \(O(n^2)\)

B. \(O(mn)\)

C. \(O(m+n)\)

D. \(O(2^n)\)

**Answer:** C

---

# One-Page Revision

- Longest path = maximum sequential dependencies before reaching a task.
- Source vertices (indegree 0) have longest path **0**.
- Compute longest paths while performing **topological sorting**.
- Update rule:

  \[
  LP(v)=\max(LP(v),LP(u)+1)
  \]

- Every edge is processed exactly once.
- Time complexity: **O(m+n)**.
- Longest path gives the **minimum completion time** for a dependency graph.
- Efficient only for **DAGs**; the general longest path problem is computationally hard.