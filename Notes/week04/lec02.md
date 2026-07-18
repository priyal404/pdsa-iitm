# Lecture 2: Representing Graphs

> **Course:** Programming, Data Structures and Algorithms using Python
>
> **Week:** Graphs
>
> **Lecture:** Representing Graphs

---

# Introduction / Overview

Graphs are often drawn as diagrams, making them easy for humans to understand. However, algorithms cannot directly work with graphical representations. To perform operations such as finding neighbours, checking reachability, or traversing a graph, we need a concrete representation that can be stored and manipulated in memory.

This lecture introduces two standard graph representations:

1. **Adjacency Matrix**
2. **Adjacency List**

and compares their advantages, disadvantages, and typical use cases. :contentReference[oaicite:0]{index=0}

---

# Main Topics

## Why Do We Need a Graph Representation?

Although a graph is usually drawn as a picture, an algorithm cannot interpret diagrams. Instead, the graph must be converted into a data structure that supports efficient computation.

To simplify representation, vertices are renamed as integers:

```text
0, 1, 2, ..., n−1
```

Thus,

- Every vertex is represented by a unique integer.
- Every edge becomes a pair of integers `(i, j)`.
- Self-loops `(i, i)` are not considered in this discussion. :contentReference[oaicite:1]{index=1}

---

## Adjacency Matrix

An **adjacency matrix** stores the graph as an **n × n** matrix.

For every pair of vertices `(i, j)`,

```text
A[i][j] = 1   if an edge exists from i to j

A[i][j] = 0   otherwise
```

Example:

|   |0|1|2|3|
|---|---|---|---|---|
|0|0|1|0|1|
|1|0|0|1|0|
|2|1|0|0|0|
|3|0|0|1|0|

A value of **1** indicates the presence of an edge, while **0** indicates its absence. :contentReference[oaicite:2]{index=2}

### Building an Adjacency Matrix

Given an edge list,

```text
[(0,1), (0,4), (4,0), ...]
```

the process is:

1. Create an `n × n` matrix initialized with zeros.
2. For every edge `(i, j)`, set

```python
A[i][j] = 1
```

This representation is straightforward and allows direct access to any edge. :contentReference[oaicite:3]{index=3}

---

## Adjacency Matrix for Undirected Graphs

In an undirected graph,

```text
(i, j) ∈ E  ⇒  (j, i) ∈ E
```

Therefore, the adjacency matrix is **symmetric** about its main diagonal.

```text
A[i][j] = A[j][i]
```

This symmetry is a useful property when working with undirected graphs. :contentReference[oaicite:4]{index=4}

---

## Finding Neighbours

The neighbours of a vertex are obtained by scanning its corresponding row in the adjacency matrix.

For vertex `i`,

- Check every column `j`.
- If `A[i][j] == 1`, then `j` is a neighbour.

Example Python logic:

```python
def neighbours(A, i):
    nbrs = []

    for j in range(len(A)):
        if A[i][j] == 1:
            nbrs.append(j)

    return nbrs
```

Thus, neighbours are found by scanning an entire row of the matrix. :contentReference[oaicite:5]{index=5}

---

## Incoming and Outgoing Edges

For **directed graphs**:

- **Rows** represent **outgoing edges**.
- **Columns** represent **incoming edges**.

```text
Row i      → Vertices reachable from i

Column i   → Vertices that can reach i
```

Unlike undirected graphs, incoming and outgoing edges are generally different. :contentReference[oaicite:6]{index=6}

---

## Degree of a Vertex

### Undirected Graph

The **degree** of a vertex is the number of edges incident on it.

It can be computed by counting the number of `1`s in its row (or column, since the matrix is symmetric).

### Directed Graph

Two separate degrees are defined:

- **In-degree:** Number of incoming edges.
- **Out-degree:** Number of outgoing edges.

In general,

```text
In-degree ≠ Out-degree
```

although they may coincide for some vertices. :contentReference[oaicite:7]{index=7}

---

## Reachability

One common graph problem is determining whether one vertex can be reached from another.

Example:

- Start from vertex **9**.
- Mark it as reachable.
- Visit all of its neighbours.
- Continue exploring neighbours of newly discovered vertices.
- Stop once the target vertex is reached.

The important idea is **never to revisit already explored vertices**, otherwise the algorithm may enter an infinite loop.

Two standard graph traversal algorithms solve this problem:

- **Breadth-First Search (BFS)** – explores level by level.
- **Depth-First Search (DFS)** – explores one path completely before backtracking.

These algorithms will be studied in later lectures. :contentReference[oaicite:8]{index=8}

---

## Adjacency List

An adjacency matrix stores information about **every possible edge**, even when most edges do not exist.

For sparse graphs, this wastes memory.

Instead, we use an **adjacency list**.

For every vertex, we store **only its neighbours**.

Example:

```text
0 → [1, 4]

1 → [2]

2 → [0, 3]

...

8 → [5, 9]
```

In Python, an adjacency list is naturally represented using a dictionary.

```python
graph = {
    0: [1, 4],
    1: [2],
    2: [0, 3]
}
```

This representation stores only existing edges, making it much more space-efficient for sparse graphs. :contentReference[oaicite:9]{index=9}

---

## Adjacency Matrix vs Adjacency List

| Feature | Adjacency Matrix | Adjacency List |
|---------|------------------|----------------|
| Storage | O(V²) | O(V + E) |
| Space Efficient | No (for sparse graphs) | Yes |
| Check if edge `(i, j)` exists | O(1) | O(degree(i)) |
| List all neighbours | O(V) | O(degree(i)) |
| Best suited for | Dense graphs | Sparse graphs |

### Trade-offs

**Adjacency Matrix**

**Advantages**

- Simple representation.
- Constant-time edge lookup.
- Easy to implement.

**Disadvantages**

- Requires large memory.
- Wastes space when the graph has few edges.
- Finding neighbours requires scanning an entire row.

---

**Adjacency List**

**Advantages**

- Requires much less memory.
- Efficient for sparse graphs.
- Listing neighbours is faster because only existing neighbours are stored.

**Disadvantages**

- Checking whether a specific edge exists requires searching the neighbour list.

For most graph algorithms studied later in the course, the adjacency list representation is generally preferred. :contentReference[oaicite:10]{index=10}

---

# Key Takeaways

- Graphs must be represented using data structures before algorithms can process them.
- Vertices are usually labelled `0` to `n−1`.
- An **adjacency matrix** uses a `0/1` matrix to represent edges.
- For undirected graphs, the adjacency matrix is symmetric.
- Rows represent outgoing edges, while columns represent incoming edges in directed graphs.
- The degree of a vertex is obtained by counting incident edges.
- Reachability can be determined by systematic graph traversal (BFS/DFS).
- An **adjacency list** stores only neighbouring vertices, making it suitable for sparse graphs.
- Choose the graph representation based on the operations that need to be performed. :contentReference[oaicite:11]{index=11}

---

# Important Formulae

### Adjacency Matrix

```text
A[i][j] =
    1, if edge (i, j) exists
    0, otherwise
```

### Maximum Number of Edges

**Undirected Graph**

```text
n(n−1)/2
```

**Directed Graph**

```text
n(n−1)
```

### Space Complexity

| Representation | Space |
|---------------|-------|
| Adjacency Matrix | O(V²) |
| Adjacency List | O(V + E) |

---

# Common GATE Questions

1. Why are graphs represented using data structures instead of diagrams?
2. What is an adjacency matrix?
3. Why is the adjacency matrix of an undirected graph symmetric?
4. What is the difference between in-degree and out-degree?
5. Compare adjacency matrix and adjacency list.
6. Which representation is preferred for sparse graphs and why?
7. What is the space complexity of an adjacency matrix?
8. Which representation provides O(1) edge lookup?

---

# Flashcards

**Q:** What does `A[i][j] = 1` represent?

**A:** An edge exists from vertex `i` to vertex `j`.

---

**Q:** Which graph representation is symmetric for undirected graphs?

**A:** Adjacency Matrix.

---

**Q:** What do rows represent in a directed adjacency matrix?

**A:** Outgoing edges.

---

**Q:** Which representation is more memory efficient for sparse graphs?

**A:** Adjacency List.

---

**Q:** Which representation provides constant-time edge lookup?

**A:** Adjacency Matrix.

---

# Practice MCQs

**Q1.** Which representation stores only neighbouring vertices?

A. Edge Matrix

B. Adjacency Matrix

C. Adjacency List

D. Incidence Matrix

**Answer:** C

---

**Q2.** The space complexity of an adjacency matrix is

A. O(V)

B. O(E)

C. O(V + E)

D. O(V²)

**Answer:** D

---

**Q3.** In a directed graph, matrix rows represent

A. Incoming edges

B. Outgoing edges

C. Degrees

D. Paths

**Answer:** B

---

**Q4.** Which representation is preferred for sparse graphs?

A. Adjacency Matrix

B. Adjacency List

C. Both equally

D. None

**Answer:** B

---

**Q5.** An adjacency matrix for an undirected graph is

A. Upper triangular

B. Lower triangular

C. Symmetric

D. Diagonal

**Answer:** C

---

# One-Page Revision

### Graph Representations

- **Adjacency Matrix:** `n × n` matrix storing 0/1 values.
- **Adjacency List:** Stores only neighbours of each vertex.

### Complexity Comparison

| Operation | Matrix | List |
|-----------|--------|------|
| Space | O(V²) | O(V + E) |
| Edge Lookup | O(1) | O(degree) |
| Neighbour Traversal | O(V) | O(degree) |

### Remember

- Undirected matrix → Symmetric.
- Rows → Outgoing edges.
- Columns → Incoming edges.
- Sparse graphs → Adjacency List.
- Dense graphs → Adjacency Matrix.
- BFS and DFS are used for graph traversal and reachability.

---