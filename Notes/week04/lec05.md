# Lecture 5: Applications of BFS and DFS

> **Course:** Programming, Data Structures and Algorithms using Python
>
> **Week:** 4
>
> **Lecture:** 5

---

# Introduction / Overview

In the previous lectures, BFS and DFS were introduced as graph traversal algorithms primarily used to determine:

- Reachability between vertices
- Recovery of paths
- Shortest paths (using BFS)

This lecture extends these ideas and explores several **structural properties of graphs** that can be efficiently discovered using BFS and DFS, including:

- Connected Components
- Cycle Detection
- DFS Numbering (Pre/Post Numbers)
- Edge Classification in Directed Graphs
- Strongly Connected Components (Introduction)

The lecture emphasizes that **DFS is considerably more powerful than BFS** for understanding the structure of a graph because it records additional information during traversal.

---

# Main Topics

# Beyond Reachability

Until now:

- **BFS**
  - Determines reachable vertices.
  - Finds shortest path (minimum number of edges).
  - Computes levels (distance from source).

- **DFS**
  - Determines reachable vertices.
  - Recovers paths using parent information.

The natural question is:

> What other information about a graph can these traversals reveal?

The answer is that graph traversals help uncover the **structure** of the graph itself.

---

# Connected Components

## Motivation

When looking at a graph visually, it is easy to identify disconnected parts.

Example:

```text
Component A        Component B

0 --- 1           2 --- 3
|                 |
4                 6

        5
```

Humans immediately notice:

- Left side is one group.
- Right side is another.
- Vertex 5 is isolated.

A computer, however, must discover these groups algorithmically.

---

## Connected Graph

An **undirected graph** is connected if:

- Every vertex can be reached from every other vertex.

Example:

```text
0 ---- 1
|      |
2 ---- 3
```

Every pair of vertices is connected through some path.

---

## Disconnected Graph

A graph is disconnected if:

- It consists of multiple independent parts.
- Some vertices cannot reach others.

Example:

```text
0 ---- 1

2 ---- 3

5
```

No path exists between the different groups.

---

## Connected Component

A **connected component** is defined as:

> A maximal set of vertices that are mutually connected.

Two important ideas:

- Every vertex inside the component is reachable from every other vertex.
- No additional vertex can be added without breaking connectivity.

Example:

```text
Component 0

0
|\
1 4
 \
 8
 |
 9
```

Another component:

```text
2
|\
3 6
| |
7 10
|
11
```

Isolated vertex:

```text
5
```

An isolated vertex also forms a connected component because it is trivially connected to itself.

---

# Finding Connected Components using BFS/DFS

Instead of running BFS only once:

- Repeat BFS (or DFS) from every unvisited vertex.

Each traversal discovers one complete component.

---

## Step 1

Start from vertex 0.

Run BFS/DFS.

Mark everything reached as:

```text
Component 0
```

---

## Step 2

Find the smallest unvisited vertex.

Suppose it is:

```text
2
```

Run BFS/DFS again.

Everything reached becomes:

```text
Component 1
```

---

## Step 3

Repeat.

Eventually:

```text
Vertex 5

↓

Component 2
```

Continue until every vertex has been visited.

---

## Algorithm

```text
component = {}

Initialize every vertex as unvisited

component_id = 0

For every vertex:

    if vertex not visited:

        Run BFS/DFS

        Mark every discovered vertex
        with current component_id

        component_id += 1
```

---

## BFS-Based Implementation Idea

The lecture uses:

```python
component[v] = -1
```

Meaning:

- `-1` → not visited yet

Maintain:

```text
component_id
```

and

```text
seen
```

where

- `seen` = number of vertices already visited.

Repeatedly:

1. Find smallest vertex whose component is `-1`.
2. Run BFS.
3. Assign current component number.
4. Increment component number.
5. Repeat until every vertex has been processed.

---

## Time Complexity

Each vertex is visited once.

Each edge is examined once.

| Algorithm | Complexity |
|-----------|------------|
| BFS Components | **O(V + E)** |
| DFS Components | **O(V + E)** |

---

# Detecting Cycles

## What is a Cycle?

A cycle is a walk that:

- Starts at a vertex.
- Ends at the same vertex.

Example:

```text
4
| \
9--8
```

Cycle:

```text
4 → 8 → 9 → 4
```

---

## Path vs Cycle

A path does **not** repeat vertices.

A cycle necessarily repeats:

- the starting vertex

Therefore,

technically,

> A cycle is a walk, not a path.

---

## Complex Cycles

Vertices may repeat.

Example:

```text
2 → 3 → 7 → 6 → 10
      |
      11
      |
      7
```

The cycle may contain repeated intermediate vertices.

However,

the same edge should **not** simply be traversed back and forth.

Example:

```text
i → j → i
```

is **not** considered a meaningful cycle.

Otherwise every edge would become a cycle.

---

## Simple Cycle

A simple cycle contains no repeated vertices except:

- first
- last

Complex cycles can often be decomposed into multiple simple cycles.

---

# Detecting Cycles using BFS

During BFS:

Whenever a new vertex is discovered:

- parent edge is recorded.

These recorded edges form:

- a tree
- or, if the graph is disconnected,
- a forest.

ASCII illustration:

```text
Tree edges

0
|
1
|
4
|
8
|
9
```

Suppose another unused edge exists:

```text
4 -------- 9
```

Adding this unused edge creates:

```text
4
| \
8  \
|   \
9----
```

which is a cycle.

---

## Important Observation

Any edge that is **not** part of the BFS tree indicates the presence of a cycle.

Thus,

for undirected graphs:

> Non-tree edge ⇒ Cycle

---

# DFS Numbering

DFS records much richer information.

Instead of merely recording parents,

DFS assigns every vertex:

- Pre number
- Post number

---

## Pre Number

Assigned when DFS first visits the vertex.

---

## Post Number

Assigned after DFS finishes exploring every descendant.

---

## Example

Suppose DFS begins at vertex 0.

```text
Visit 0

pre(0)=0
```

Move to 1

```text
pre(1)=1
```

Vertex 1 finishes immediately

```text
post(1)=2
```

Return to 0.

Explore 4.

```text
pre(4)=3
```

Explore 8.

```text
pre(8)=4
```

Explore 9.

```text
pre(9)=5
```

Now backtracking begins.

```text
post(9)=6

post(8)=7

post(4)=8

post(0)=9
```

The numbering continues across components instead of restarting.

---

## Important Property

Every vertex satisfies:

```text
pre(v) < post(v)
```

---

# DFS Implementation with Pre/Post Numbers

Maintain three dictionaries:

```python
visited

pre

post
```

Initially:

```python
visited[v] = False

pre[v] = -1

post[v] = -1
```

Maintain one global counter.

Whenever DFS enters a vertex:

```python
pre[v] = counter

counter += 1
```

After recursively exploring neighbors:

```python
post[v] = counter

counter += 1
```

Thus,

every DFS call performs:

```text
Assign Pre

↓

Explore Children

↓

Assign Post
```

---

# Cycle Detection using DFS

DFS also creates a tree (or forest).

Every edge belongs to either:

- DFS tree
- Non-tree edge

For undirected graphs,

every non-tree edge produces a cycle.

---

# Edge Classification in Directed Graphs

In directed graphs,

not every non-tree edge creates a cycle.

DFS classifies non-tree edges into three categories.

---

## 1. Forward Edge

Connects:

Ancestor → Descendant

Example:

```text
0

↓

1

↓

4

↓

5
```

Additional edge:

```text
0 → 5
```

Still points downward.

---

## 2. Back Edge

Connects:

Descendant → Ancestor

Example:

```text
5 → 1
```

This returns upward in the DFS tree.

These edges create cycles.

---

## 3. Cross Edge

Connects two unrelated branches.

Example:

```text
3 → 6
```

or

```text
6 → 7
```

Neither endpoint is an ancestor of the other.

---

## Summary

| Edge Type | Direction | Creates Cycle? |
|-----------|-----------|----------------|
| Tree | Parent → Child | No |
| Forward | Ancestor → Descendant | No |
| Back | Descendant → Ancestor | Yes |
| Cross | Between branches | No |

---

# Using Pre/Post Numbers to Classify Edges

The interval

```text
[pre(v), post(v)]
```

represents the period during which DFS is processing vertex `v`.

---

## Forward Edge

If

```text
Interval(v)
```

lies completely inside

```text
Interval(u)
```

then

```text
u
```

is an ancestor of

```text
v
```

Therefore:

```text
u → v
```

is a forward (or tree) edge.

---

## Back Edge

If

```text
u
```

lies inside

```text
v
```

then

```text
u → v
```

moves upward.

Hence it is a back edge.

---

## Cross Edge

Intervals are disjoint.

Example:

```text
[4,8]

[12,17]
```

The two DFS explorations happened independently.

Hence,

the edge connects different branches.

---

## Why Pre/Post Numbers Matter

These numbers allow DFS to determine:

- ancestor-descendant relationships
- edge classification
- cycle detection
- graph structure

without explicitly storing every traversal path.

---

# Strongly Connected Components (Introduction)

Connectivity in directed graphs is more restrictive.

Two vertices are strongly connected only if:

```text
u → v

AND

v → u
```

Both directions must be possible.

---

## Strongly Connected Component (SCC)

A maximal group of vertices where:

Every vertex can reach every other vertex.

Example:

```text
0 → 1 → 2
↑       ↓
←-------
```

These belong to one SCC.

However,

if only

```text
0 → 1
```

exists,

they are **not** strongly connected.

---

## Computing SCCs

The lecture briefly notes that:

DFS numbering can also be used to compute:

- Strongly Connected Components

Detailed algorithms are covered later (e.g., Kosaraju's or Tarjan's algorithms), so their implementation is beyond the scope of this lecture.

---

# Why DFS is Preferred

Compared to BFS,

DFS provides much richer structural information.

DFS numbering can be used for:

- Connected components
- Cycle detection
- Edge classification
- Strongly connected components
- Graph structure analysis
- Critical vertices and bridges (mentioned as future applications)

Because of this,

DFS is often the preferred traversal algorithm for advanced graph algorithms.

---

# Key Takeaways

- BFS and DFS can do much more than checking reachability.
- Connected components are found by repeatedly running BFS/DFS from unvisited vertices.
- Connected components divide an undirected graph into maximal connected subgraphs.
- BFS and DFS produce spanning trees (or forests).
- In undirected graphs, every non-tree edge indicates a cycle.
- DFS assigns each vertex **pre** and **post** numbers.
- Pre/Post numbering captures the order in which DFS enters and exits vertices.
- Directed graph edges can be classified into tree, forward, back, and cross edges.
- Only **back edges** indicate cycles in directed graphs.
- DFS numbering forms the basis of many advanced graph algorithms, including Strongly Connected Components.

---

# Important Formulae

### Connected Components

Repeated BFS/DFS:

\[
O(V+E)
\]

---

### DFS Traversal

\[
O(V+E)
\]

---

### BFS Traversal

\[
O(V+E)
\]

---

### DFS Numbering Property

For every vertex:

\[
pre(v) < post(v)
\]

---

# GATE / Interview Focus

## Must Remember

- Connected components are computed by repeatedly running BFS/DFS on unvisited vertices.
- A connected graph has exactly **one** connected component.
- An isolated vertex forms its own connected component.
- BFS and DFS generate spanning trees (or forests).
- In **undirected graphs**, every non-tree edge forms a cycle.
- In **directed graphs**, only **back edges** indicate cycles.
- DFS assigns both **pre** and **post** numbers.
- Pre/Post intervals reveal ancestor–descendant relationships.
- Strongly connected means reachability in **both** directions.

---

# Common GATE Questions

### Q1. How can connected components be found?

**Answer:**

Run BFS or DFS repeatedly from every unvisited vertex. Each traversal identifies one connected component.

---

### Q2. Why are pre and post numbers useful?

**Answer:**

They record the order in which DFS enters and exits vertices, enabling edge classification and ancestor-descendant detection.

---

### Q3. Which edge type creates a cycle in a directed graph?

**Answer:**

Only **back edges**.

---

### Q4. What is the difference between connected and strongly connected graphs?

**Answer:**

A connected graph (undirected) requires every pair of vertices to be reachable. A strongly connected directed graph requires reachability in **both directions** for every pair of vertices.

---

# Flashcards

**Q:** What is a connected component?

**A:** A maximal set of mutually connected vertices.

---

**Q:** How are connected components computed?

**A:** By repeatedly running BFS/DFS from unvisited vertices.

---

**Q:** What numbers does DFS assign to each vertex?

**A:** Pre number and Post number.

---

**Q:** Which edge indicates a cycle in a directed graph?

**A:** A back edge.

---

**Q:** What does a forward edge connect?

**A:** An ancestor to one of its descendants.

---

**Q:** What does a cross edge connect?

**A:** Two different branches of the DFS forest.

---

**Q:** What is a strongly connected component?

**A:** A maximal set of vertices where every vertex is reachable from every other vertex.

---

# Practice MCQs

### Q1. A connected undirected graph contains how many connected components?

A. 0

B. 1

C. V

D. E

**Answer:** **B**

---

### Q2. DFS assigns which two numbers to every vertex?

A. Parent and Level

B. Distance and Parent

C. Pre and Post

D. Degree and Weight

**Answer:** **C**

---

### Q3. Which edge type indicates a cycle in a directed graph?

A. Tree Edge

B. Forward Edge

C. Cross Edge

D. Back Edge

**Answer:** **D**

---

### Q4. The time complexity of finding connected components using BFS is:

A. O(V²)

B. O(E²)

C. O(V + E)

D. O(log V)

**Answer:** **C**

---

### Q5. Two vertices belong to the same strongly connected component if:

A. One can reach the other.

B. They have the same degree.

C. Each can reach the other.

D. They are in the same DFS tree.

**Answer:** **C**

---

# One-Page Revision

- BFS computes reachability, shortest paths, and levels.
- DFS computes reachability and richer structural information.
- Connected Component = maximal connected subgraph.
- Find components by repeatedly running BFS/DFS on unvisited vertices.
- BFS/DFS generate spanning trees (or forests).
- In undirected graphs:
  - Non-tree edge ⇒ Cycle.
- DFS assigns:
  - **Pre number** (entry time)
  - **Post number** (exit time)
- Edge types in directed graphs:
  - Tree
  - Forward
  - Back ✅ (forms cycles)
  - Cross
- Pre/Post intervals determine ancestor–descendant relationships.
- Strongly Connected Components require reachability in **both** directions.
- DFS numbering is the foundation for advanced graph algorithms such as SCC detection, bridges, and articulation points.