# Lecture 04: Depth First Search (DFS)

> **Course:** Programming Data Structures and Algorithms using Python
>
> **Week:** Graph Algorithms
>
> **Lecture:** Depth First Search (DFS)

---

# Introduction

Depth First Search (DFS) is the second fundamental graph traversal technique after Breadth First Search (BFS).

Unlike BFS, which explores vertices **level by level**, DFS explores **one path completely before backtracking**. This strategy is useful for discovering the structural properties of a graph and forms the basis for many advanced graph algorithms.

---

# Main Topics

## DFS Intuition

The idea behind DFS is simple:

1. Start from a source vertex.
2. Visit one unvisited neighbour.
3. Continue moving deeper into the graph.
4. Stop only when no unexplored neighbour exists.
5. Backtrack to the most recent vertex with unexplored neighbours.
6. Repeat until every reachable vertex has been explored.

Unlike BFS, DFS does **not** explore all neighbours immediately.

Instead, it keeps following a single path.

### Example

```text
A
|
B
|
C
|
D
```

DFS visits

```text
A → B → C → D
```

instead of exploring every neighbour at each level.

---

## Backtracking

Whenever DFS reaches a dead end,

```text
Current Vertex
      |
No unvisited neighbour
      |
Backtrack
```

it returns to the **most recently visited unfinished vertex**.

This systematic backtracking is what gives DFS its name.

---

## DFS Uses a Stack

Unlike BFS, which uses a **Queue (FIFO)**,

DFS uses a **Stack (LIFO)**.

```text
Push

A
↓

A
B
↓

A
B
C

Pop

Remove C
↓

A
B
```

The last vertex inserted into the stack is processed first.

This naturally supports backtracking.

---

## DFS Example

Suppose DFS starts from vertex **4**.

Neighbours:

```text
4 → {0, 3, 7}
```

Assume neighbours are explored in increasing order.

Traversal proceeds as

```text
4
↓

0
↓

1
↓

2
```

Vertex **2** has no unvisited neighbours.

Backtrack:

```text
2 ← 1 ← 0 ← 4
```

Continue exploring remaining neighbours:

```text
4
↓

3
↓

5
↓

6
```

Backtrack again:

```text
6 ← 5
```

Then continue

```text
5
↓

7
↓

8
↓

9
```

Finally,

```text
9 ← 8 ← 7 ← 5 ← 3 ← 4
```

The traversal finishes when the stack becomes empty.

---

## DFS Using Recursion

Instead of explicitly maintaining a stack, recursion can be used.

Each recursive function call is automatically placed on the **call stack**, providing the same behaviour as an explicit stack.

Thus,

```text
DFS(A)

↓

DFS(B)

↓

DFS(C)

↓

DFS(D)
```

When `D` finishes,

```text
Return to C

↓

Return to B

↓

Return to A
```

This implicit stack performs the required backtracking automatically.

---

## Initialization

Before starting DFS,

```python
visited[v] = False
parent[v] = -1
```

for every vertex.

The source vertex is then explored recursively.

---

## Recursive DFS Algorithm

```python
DFS(G, v)

visited[v] = True

for each neighbour k of v:

    if not visited[k]:

        parent[k] = v

        DFS(G, k)
```

The algorithm:

- Marks the current vertex as visited.
- Explores every unvisited neighbour recursively.
- Returns automatically when no neighbour remains.

---

## Global vs Local Variables

Two implementations are possible.

### 1. Local Version

`visited` and `parent` are passed as function arguments.

```python
DFS(G, v, visited, parent)
```

Every recursive call returns updated dictionaries.

---

### 2. Global Version

`visited` and `parent` are declared globally.

```python
visited = {}
parent = {}
```

Recursive calls directly modify these shared structures.

Advantages:

- Simpler code
- No need to repeatedly pass large dictionaries
- Common implementation in practice

---

## DFS with Adjacency Matrix

Neighbours are found by scanning an entire row.

Exploration of one vertex requires

```text
O(n)
```

time.

Overall complexity:

```text
O(n²)
```

---

## DFS with Adjacency List

Neighbours are already stored.

Only actual neighbours are visited.

Total exploration cost equals the sum of all vertex degrees.

Using

```text
Σ degree(v) = 2m
```

the total complexity becomes

```text
O(n + m)
```

which is optimal for sparse graphs.

---

## Complexity Analysis

| Representation | Time Complexity |
|---------------|-----------------|
| Adjacency Matrix | O(n²) |
| Adjacency List | O(n + m) |

Each vertex is

- visited once
- explored once

Every edge is examined only when exploring its incident vertex.

---

## DFS vs BFS

| BFS | DFS |
|------|------|
| Queue | Stack / Recursion |
| Level-by-level | Path-by-path |
| Finds shortest path (unweighted) | Does **not** guarantee shortest path |
| Explores neighbours first | Explores one branch completely |

Example:

```text
0
|\
| \
1--2
```

DFS may discover

```text
0 → 1 → 2
```

even though

```text
0 → 2
```

is shorter.

Thus, the DFS tree does **not** necessarily represent shortest paths.

---

## Why Use DFS?

Although DFS cannot find shortest paths, it provides valuable structural information about graphs.

Many advanced graph algorithms are based on DFS, including:

- Cycle detection
- Topological sorting
- Connected components
- Strongly Connected Components (SCCs)
- Articulation points and bridges

These applications are explored in later lectures.

---

# Key Takeaways

- DFS explores one branch completely before backtracking.
- Backtracking is naturally implemented using a stack or recursion.
- Every vertex is visited exactly once.
- Parent information can reconstruct one traversal path.
- DFS does **not** guarantee shortest paths.
- Time complexity is **O(n²)** with an adjacency matrix and **O(n + m)** with an adjacency list.

---

# Important Formulae

### Sum of Degrees

```text
Σ degree(v) = 2m
```

### Time Complexity

| Representation | Complexity |
|---------------|------------|
| Adjacency Matrix | O(n²) |
| Adjacency List | O(n + m) |

---

# GATE / Interview Focus

- DFS uses a **Stack (LIFO)** or recursion.
- Understand recursive DFS implementation.
- Difference between explicit stack and recursion.
- DFS does not compute shortest paths.
- Compare DFS and BFS.
- Complexity using adjacency matrix vs adjacency list.
- Applications of DFS in graph algorithms.

---

# Common GATE Questions

1. Why is recursion suitable for DFS?
2. Why does DFS use a stack while BFS uses a queue?
3. Does DFS always find the shortest path?
4. Compare DFS using adjacency matrix and adjacency list.
5. Explain the role of the `parent` array in DFS.
6. What is the time complexity of DFS?

---

# Flashcards

**Q:** Which data structure does DFS use?

**A:** Stack (or the recursion call stack).

---

**Q:** When does DFS backtrack?

**A:** When the current vertex has no unexplored neighbours.

---

**Q:** Does DFS always find the shortest path?

**A:** No.

---

**Q:** Why is recursion commonly used for DFS?

**A:** The function call stack naturally behaves like a stack.

---

**Q:** What is the complexity of DFS using an adjacency list?

**A:** O(n + m)

---

# Practice MCQs

### Q1.

DFS primarily uses

A. Queue

B. Stack

C. Heap

D. Priority Queue

**Answer:** B

---

### Q2.

DFS explores

A. Level by level

B. Randomly

C. One branch completely before backtracking

D. Lowest-degree vertex first

**Answer:** C

---

### Q3.

Recursive DFS relies on

A. Queue

B. Heap

C. Call Stack

D. Linked List

**Answer:** C

---

### Q4.

DFS guarantees shortest paths in

A. Weighted graphs

B. Directed graphs

C. Unweighted graphs

D. None of these

**Answer:** D

---

### Q5.

DFS using an adjacency list runs in

A. O(n²)

B. O(n + m)

C. O(m²)

D. O(log n)

**Answer:** B

---

# One-Page Revision

## Depth First Search

- Explores one path completely before backtracking.
- Uses **Stack (LIFO)** or recursion.
- Visits every reachable vertex once.

---

### Steps

```text
Visit

↓

Choose one neighbour

↓

Go deeper

↓

Dead end?

↓

Backtrack
```

---

### Complexity

| Representation | Time |
|---------------|------|
| Adjacency Matrix | O(n²) |
| Adjacency List | O(n + m) |

---

### DFS vs BFS

| BFS | DFS |
|------|------|
| Queue | Stack |
| Level-wise | Depth-wise |
| Shortest path | No shortest path guarantee |

---

### Applications

- Graph traversal
- Cycle detection
- Topological sorting
- Connected Components
- SCCs
- Bridges & Articulation Points

---