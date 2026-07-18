# Lecture 01: Introduction to Graphs

> **Course:** Programming, Data Structures and Algorithms using Python
>
> **Week:** 4
>
> **Lecture:** 1

---

# What is a Graph?

A **graph** is a mathematical structure used to represent **relationships** between objects.

Instead of storing data sequentially like arrays or lists, graphs focus on **connections**.

A graph consists of:

- **Vertices (Nodes)** → represent objects.
- **Edges** → represent relationships between objects.

Example:

Teachers and courses.

- Vertices represent teachers and courses.
- An edge connects a teacher to a course they teach.

```
Teacher A ------> Python

Teacher B ------> Data Structures

Teacher C ------> Algorithms
```

Here, the edge represents the relationship:

> "Teacher teaches Course."

Graphs are widely used because many real-world problems involve relationships rather than sequences. :contentReference[oaicite:0]{index=0}

---

# Graph as a Relation

A graph can be viewed as a **binary relation**.

Suppose:

- **T** = Set of teachers
- **C** = Set of courses

The teaching assignment is a subset of:

```
T × C
```

Each edge corresponds to one ordered pair:

```
(Teacher, Course)
```

For example,

```
(Alice, Python)

(Bob, Algorithms)
```

Only the existing relationships are represented as edges.

---

# Vertices (Nodes)

Vertices (also called **nodes**) represent the entities involved in the problem.

Examples:

- People
- Cities
- Computers
- Courses
- Web pages

Graph notation:

```
G = (V, E)
```

where

- **V** = Set of vertices
- **E** = Set of edges

Normally,

a vertex is **not connected to itself**.

Such graphs are said to be **irreflexive**. :contentReference[oaicite:1]{index=1}

---

# Directed Graphs

A **directed graph (digraph)** has edges with directions.

```
A -----> B
```

means

```
A → B
```

does **not** imply

```
B → A
```

Example:

Teacher teaches Course.

```
Teacher -----> Course
```

A course cannot teach a teacher.

Hence,

the direction matters.

Directed graphs are useful for representing:

- Airline routes
- Dependencies
- Web links
- Task scheduling
- Teacher-course assignments :contentReference[oaicite:2]{index=2}

---

# Undirected Graphs

Some relationships are naturally **symmetric**.

Example:

Friendship.

If

```
Alice is Bob's friend
```

then

```
Bob is Alice's friend.
```

Instead of drawing two arrows,

```
A ---> B

B ---> A
```

we simply draw

```
A ------- B
```

Such graphs are called **undirected graphs**.

The edge can be traversed in **both directions**.

Examples:

- Friendships
- Road networks
- Social networks
- Computer LAN connections :contentReference[oaicite:3]{index=3}

---

# Paths in a Graph

A **path** is a sequence of connected edges that allows us to travel from one vertex to another.

Example:

```
A ---- B ---- C ---- D
```

Path from A to D:

```
A → B → C → D
```

Multiple paths may exist between the same pair of vertices.

For example,

```
A → B → D

A → C → D
```

Both connect A to D using different intermediate vertices.

Paths are useful for modeling:

- Travel routes
- Communication paths
- Data transmission
- Social connections :contentReference[oaicite:4]{index=4}

---

# Path vs Walk

A **path** does **not** repeat vertices.

Example of a path:

```
A → B → C → D
```

Every vertex appears only once.

---

A **walk** may revisit the same vertex multiple times.

Example:

```
A → B → C → B → D
```

Since vertex **B** is visited twice,

this is **not** a path.

It is called a **walk**. :contentReference[oaicite:5]{index=5}

---

# Paths in Directed Graphs

In a directed graph,

paths must follow the direction of the arrows.

Example:

```
A → B → C
```

Valid path:

```
A → B → C
```

Invalid path:

```
C → B → A
```

because the arrows point in the opposite direction.

A real-world example is an airline route network, where flights operate only in specific directions. :contentReference[oaicite:6]{index=6}

---

# Graph Colouring

One of the most important applications of graphs is solving **graph colouring problems**.

The lecture begins by introducing a practical example: **map colouring**.

Suppose we have a map containing several neighbouring states or countries.

Our objective is to colour the map such that:

- No two neighbouring regions have the same colour.
- The total number of colours used is as small as possible.

For example,

```text
+---------+---------+
| State A | State B |
+---------+---------+
| State C | State D |
+---------+---------+
```

Since neighbouring states share borders, they cannot have identical colours.

Instead of solving the problem directly on the geographical map, we first convert it into a graph.

---

# Converting a Map into a Graph

To transform a map-colouring problem into a graph:

1. Represent every state (or country) as a **vertex**.
2. Draw an **edge** between two vertices if the corresponding states share a common border.

Example:

```text
      A
     / \
    B---C
     \
      D
```

Here,

- Vertices represent states.
- Edges represent shared boundaries.

Notice that the actual shape, size, and orientation of the states no longer matter.

The graph preserves only the information that is important:

> **Which regions are neighbours?**

This abstraction is one of the greatest strengths of graph modelling.

Different drawings of the same graph may look different, yet represent exactly the same relationships.

For example,

```text
A-----B
 \   /
  \ /
   C
```

and

```text
   A

B      C
 \    /
  \  /
   \/
```

represent the same graph if the connectivity remains unchanged.

Thus, graph algorithms depend only on **adjacency**, not on geometry or physical layout. :contentReference[oaicite:0]{index=0}

---

# The Graph Colouring Problem

After converting the map into a graph, the problem becomes much more general.

We are now given:

- A graph
- A set of available colours

Our objective is to assign colours to vertices such that

> No two adjacent vertices have the same colour.

Formally,

If

```text
(u, v) ∈ E
```

then

```text
Colour(u) ≠ Colour(v)
```

Example:

```text
      Red
       A
      / \
     /   \
 Blue B---C Green
```

This colouring is valid because no adjacent vertices share the same colour.

However,

```text
      Red
       A
      / \
     /   \
 Red B---C Green
```

is invalid because vertices **A** and **B** are connected by an edge but have the same colour. :contentReference[oaicite:1]{index=1}

---

# Planar Graphs and the Four Colour Theorem

A graph is called **planar** if it can be drawn on a plane without any edges crossing each other.

Example of a planar graph:

```text
      A
     / \
    B---C
```

Example of a drawing that appears non-planar:

```text
A ----- C
 \     /
  \   /
   \ /
   / \
  /   \
 /     \
B ----- D
```

Sometimes edges cross simply because of the way the graph is drawn.

By rearranging the vertices, the same graph may be drawn without any crossings.

The lecture emphasizes that **edge crossings in a drawing do not necessarily mean that the graph is non-planar**.

A famous theorem in graph theory states:

> **Every planar graph can be coloured using at most four colours.**

This is known as the **Four Colour Theorem**.

Consequently, every geographical map can always be coloured using four colours.

For **non-planar graphs**, however, determining the minimum number of colours becomes a difficult computational problem, and no efficient algorithm is known for solving it in the general case. :contentReference[oaicite:2]{index=2}

---

# Application: Classroom Scheduling

Graph colouring is useful far beyond geographical maps.

The lecture presents the example of scheduling classrooms in a school or college.

Suppose the timetable is:

```text
Time →

Math
|-------------|

English
      |--------------|

History
             |-----------|

Science
             |---------------|
```

Some classes overlap in time.

Two overlapping classes **cannot** be assigned to the same classroom.

---

## Converting the Scheduling Problem into a Graph

Each class is represented as a vertex.

Two classes are connected by an edge if their timings overlap.

Example:

```text
Math -------- English
               /    \
              /      \
        History------Science
```

Here,

- An edge means the two classes cannot share a classroom.
- No edge means they can potentially use the same classroom.

Now the problem becomes exactly the graph colouring problem.

- Vertices → Classes
- Colours → Classrooms

If two vertices are adjacent, they must receive different colours.

Suppose the colouring is

| Class | Classroom |
|--------|-----------|
| Math | Room 1 |
| English | Room 2 |
| History | Room 1 |
| Science | Room 3 |

Notice that **Math** and **History** reuse the same classroom because they do not overlap in time.

Thus, even though there are four classes, only **three classrooms** are required.

This illustrates how graph colouring helps optimize resource allocation problems. :contentReference[oaicite:3]{index=3}

---

# Vertex Cover

The lecture next introduces another fundamental graph problem through the example of **placing security cameras in a hotel**.

Suppose:

- Corridor intersections are represented as vertices.
- Corridors themselves are represented as edges.

```text
A ----- B
|       |
|       |
C ----- D
```

A security camera placed at an intersection can monitor **all corridors incident on that intersection**.

Our objective is:

> Monitor every corridor while using the minimum number of cameras.

---

## Definition

A **Vertex Cover** is a set of vertices such that every edge has at least one endpoint belonging to the set.

Example:

```text
A ----- B
|       |
|       |
C ----- D
```

Suppose cameras are placed at **B** and **C**.

Every corridor touches either B or C.

Therefore,

```text
{B, C}
```

is a valid vertex cover.

Our goal is to find the **minimum vertex cover**, i.e., the smallest possible set of vertices satisfying this property.

Applications include:

- CCTV placement
- Network monitoring
- Sensor deployment
- Road surveillance
- Communication infrastructure monitoring

The lecture emphasizes that placing a camera at every intersection is always possible but wasteful. The computational challenge is to minimize the number of cameras while still monitoring every corridor. :contentReference[oaicite:4]{index=4}

---

# Independent Set

The next application involves scheduling cultural performances.

Suppose each dance performance is represented by a vertex.

Two performances are connected by an edge if they require at least one common performer.

```text
Dance A ----- Dance B
     |
     |
Dance C
```

If two performances share a performer, they cannot both be scheduled at the same time.

---

## Definition

An **Independent Set** is a set of vertices such that **no two selected vertices are connected by an edge**.

Example:

```text
A ----- B

C ----- D
```

Possible independent sets include

```text
{A, D}
```

or

```text
{B, C}
```

because none of the selected vertices are adjacent.

The computational objective is to find the **Maximum Independent Set**, i.e., the largest independent set in the graph.

Applications include:

- Event scheduling
- Resource allocation
- Wireless communication
- Conflict-free task selection

Unlike Vertex Cover, where every edge must be covered, here we wish to select as many mutually non-conflicting vertices as possible. :contentReference[oaicite:5]{index=5}

---

# Matching

The final major concept introduced in this lecture is **Matching**.

Suppose students are to be assigned project partners.

Two students can work together only if they are friends.

Represent:

- Students → Vertices
- Friendship → Edges

```text
A ----- B

C ----- D

E ----- F
```

Each selected edge represents one project group.

However,

- No student may belong to more than one pair.

Therefore, selected edges cannot share endpoints.

---

## Definition

A **Matching** is a set of edges such that no two selected edges share a common vertex.

Example:

```text
A ----- B

C ----- D

E ----- F
```

Choosing

```text
(A, B)

(C, D)

(E, F)
```

forms a matching.

---

## Maximal Matching vs Maximum Matching

The lecture distinguishes between two commonly confused terms.

### Maximal Matching

A matching that **cannot be extended** by adding another edge.

It is not necessarily the largest possible matching.

### Maximum Matching

A matching containing the **largest possible number of edges**.

Every maximum matching is maximal, but not every maximal matching is maximum.

For project allocation, maximum matching ensures that the largest possible number of students are paired with partners.

Applications include:

- Student project allocation
- Job assignment
- Marriage problem
- Network resource allocation
- Bipartite graph optimization

Finding maximum matchings is one of the most important problems in graph algorithms and has numerous practical applications. :contentReference[oaicite:6]{index=6}

---

# Lecture Summary

This lecture introduced graphs as a universal tool for representing relationships between objects.

The key concepts covered include:

- Graphs as representations of binary relations.
- Vertices and edges.
- Directed and undirected graphs.
- Paths, walks, and reachability.
- Connected graphs.
- Graph colouring and its applications.
- Planar graphs and the Four Colour Theorem.
- Classroom scheduling using graph colouring.
- Vertex Cover.
- Independent Set.
- Matching and maximum matching.

These concepts provide the foundation for almost every graph algorithm studied later, including graph traversal, shortest paths, minimum spanning trees, network flow, and many optimization problems.

---

# Key Takeaways

- A **graph** is a mathematical structure used to model relationships between objects.
- A graph consists of **vertices (nodes)** and **edges**.
- Graphs provide a flexible abstraction that allows many real-world problems to be represented in a common form.
- Graphs can be classified as:
  - **Directed Graphs (Digraphs)** — edges have a specific direction.
  - **Undirected Graphs** — edges can be traversed in both directions.
- A graph can be viewed as a **binary relation**, where edges represent relationships between pairs of vertices.
- A **path** is a sequence of connected edges that does not revisit any vertex.
- A **walk** may revisit vertices and is therefore more general than a path.
- In directed graphs, every path must follow the direction of the edges.
- A vertex is **reachable** if there exists a path from another vertex to it.
- A graph is **connected** if every vertex can reach every other vertex.
- Many practical problems can be converted into graph problems, including:
  - Map colouring
  - Classroom scheduling
  - Security camera placement
  - Event scheduling
  - Student pairing
- **Graph Colouring** assigns colours to vertices such that adjacent vertices have different colours.
- **Planar Graphs** can always be coloured using at most **four colours** (Four Colour Theorem).
- A **Vertex Cover** is a set of vertices that covers every edge.
- An **Independent Set** is a set of vertices with no edges between any pair.
- A **Matching** is a set of edges where no two edges share a common endpoint.
- **Maximum Matching** finds the largest possible matching, while **Maximal Matching** simply cannot be extended further.

---

# Important Formulae

Although this lecture is primarily conceptual, the following formal definitions are important.

## Graph

```text
G = (V, E)
```

where

- **V** = Set of Vertices
- **E** = Set of Edges

---

## Binary Relation

```text
E ⊆ V × V
```

The edge set is a subset of all possible ordered pairs of vertices.

---

## Graph Colouring Constraint

For every edge

```text
(u, v) ∈ E
```

the colouring must satisfy

```text
Colour(u) ≠ Colour(v)
```

---

## Vertex Cover

A set

```text
S ⊆ V
```

is a vertex cover if every edge has at least one endpoint in **S**.

---

## Independent Set

A set

```text
S ⊆ V
```

is an independent set if no two vertices in **S** are adjacent.

---

## Matching

A matching is a subset of edges such that no two selected edges share a common vertex.

---

# GATE / Interview Focus

## Must Remember

### Graph Basics

- Graph = Vertices + Edges.
- Vertices are also called **nodes**.
- Edges represent relationships.

---

### Directed vs Undirected Graph

| Directed Graph | Undirected Graph |
|----------------|------------------|
| Edges have direction | Edges have no direction |
| Movement follows arrows | Movement possible in both directions |
| Example: Airline Routes | Example: Friendship |

---

### Path vs Walk

| Path | Walk |
|------|------|
| No repeated vertices | Repeated vertices allowed |
| Simpler traversal | General traversal |

This distinction is frequently tested in examinations.

---

### Reachability

A node is reachable if **at least one valid path exists**.

Many graph algorithms are based entirely on solving reachability problems.

---

### Connected Graph

A graph is connected if every vertex is reachable from every other vertex.

Removing an edge does **not necessarily** disconnect a graph if an alternate path exists.

---

### Graph Colouring

Remember:

- Vertices receive colours.
- Adjacent vertices cannot have the same colour.
- Used for scheduling, resource allocation, register allocation, timetable generation, and map colouring.

---

### Four Colour Theorem

Every **planar graph** can be coloured using **at most four colours**.

This theorem applies specifically to planar graphs.

---

### Vertex Cover

Think:

> Cover every edge using the fewest vertices.

Typical applications:

- CCTV placement
- Sensor placement
- Monitoring road networks

---

### Independent Set

Think:

> Select the maximum number of mutually non-conflicting vertices.

Typical applications:

- Event scheduling
- Resource allocation
- Conflict-free task selection

---

### Matching

Think:

> Pair vertices without sharing endpoints.

Applications include:

- Student project allocation
- Job assignment
- Stable matching
- Network pairing problems

---

# Common GATE Questions

### Q1. What is the difference between a directed graph and an undirected graph?

**Answer:**

A directed graph has edges with a specific direction, whereas an undirected graph treats every edge as bidirectional.

---

### Q2. What is the difference between a path and a walk?

**Answer:**

A path does not repeat any vertex, whereas a walk may revisit vertices.

---

### Q3. What is reachability?

**Answer:**

A vertex is reachable from another vertex if there exists at least one path connecting them.

---

### Q4. What makes a graph connected?

**Answer:**

A graph is connected if every vertex is reachable from every other vertex.

---

### Q5. What is graph colouring?

**Answer:**

Assigning colours to vertices such that adjacent vertices receive different colours.

---

### Q6. State the Four Colour Theorem.

**Answer:**

Every planar graph can be coloured using at most four colours.

---

### Q7. What is a Vertex Cover?

**Answer:**

A set of vertices such that every edge has at least one endpoint in the set.

---

### Q8. What is an Independent Set?

**Answer:**

A set of vertices in which no two vertices are adjacent.

---

### Q9. What is the difference between maximal matching and maximum matching?

**Answer:**

A maximal matching cannot be extended by adding another edge, whereas a maximum matching contains the largest possible number of edges.

---

### Q10. Give one practical application of graph colouring.

**Answer:**

Classroom scheduling, timetable generation, register allocation, frequency assignment, or map colouring.

---

# Flashcards

### Flashcard 1

**Q:** What are the two components of a graph?

**A:** Vertices and edges.

---

### Flashcard 2

**Q:** What is another name for a vertex?

**A:** Node.

---

### Flashcard 3

**Q:** What does an edge represent?

**A:** A relationship between two vertices.

---

### Flashcard 4

**Q:** What is a directed graph?

**A:** A graph whose edges have directions.

---

### Flashcard 5

**Q:** What is an undirected graph?

**A:** A graph whose edges can be traversed in both directions.

---

### Flashcard 6

**Q:** What is a path?

**A:** A sequence of connected edges that does not revisit any vertex.

---

### Flashcard 7

**Q:** What is a walk?

**A:** A sequence of connected edges that may revisit vertices.

---

### Flashcard 8

**Q:** What is reachability?

**A:** The existence of a path from one vertex to another.

---

### Flashcard 9

**Q:** What is a connected graph?

**A:** A graph where every vertex is reachable from every other vertex.

---

### Flashcard 10

**Q:** What is graph colouring?

**A:** Assigning colours to vertices so adjacent vertices have different colours.

---

### Flashcard 11

**Q:** What is a planar graph?

**A:** A graph that can be drawn without crossing edges.

---

### Flashcard 12

**Q:** What is the Four Colour Theorem?

**A:** Every planar graph can be coloured with at most four colours.

---

### Flashcard 13

**Q:** What is a Vertex Cover?

**A:** A set of vertices covering every edge.

---

### Flashcard 14

**Q:** What is an Independent Set?

**A:** A set of mutually non-adjacent vertices.

---

### Flashcard 15

**Q:** What is a Matching?

**A:** A set of edges where no two selected edges share a common endpoint.

---

# Practice MCQs

### Q1. A graph consists of

A. Vertices only

B. Edges only

C. Vertices and Edges

D. Nodes only

**Answer:** C

---

### Q2. Which of the following represents a symmetric relationship?

A. Airline Routes

B. Teacher teaches Course

C. Friendship

D. Parent → Child

**Answer:** C

---

### Q3. Which graph has edges with directions?

A. Complete Graph

B. Undirected Graph

C. Directed Graph

D. Tree

**Answer:** C

---

### Q4. Which statement is true about a path?

A. Vertices may repeat.

B. Every edge must have weight 1.

C. Vertices are not repeated.

D. Edges cannot intersect.

**Answer:** C

---

### Q5. A graph is connected if

A. Every vertex has degree 2.

B. Every edge has weight 1.

C. Every vertex is reachable from every other vertex.

D. Every graph has a cycle.

**Answer:** C

---

### Q6. Which problem is solved using graph colouring?

A. Binary Search

B. Classroom Scheduling

C. Matrix Multiplication

D. Heap Construction

**Answer:** B

---

### Q7. The Four Colour Theorem applies to

A. Complete Graphs

B. Directed Graphs

C. Planar Graphs

D. Trees

**Answer:** C

---

### Q8. Which graph problem models security camera placement?

A. Matching

B. Independent Set

C. Vertex Cover

D. Minimum Spanning Tree

**Answer:** C

---

### Q9. Which graph problem models conflict-free event scheduling?

A. Matching

B. Independent Set

C. Vertex Cover

D. Shortest Path

**Answer:** B

---

### Q10. Which graph problem is commonly used for assigning project partners?

A. Graph Colouring

B. Matching

C. BFS

D. DFS

**Answer:** B

---

# One-Page Revision

## Graph Basics

- Graph = **Vertices + Edges**
- Vertices = Nodes
- Edges = Relationships

---

## Types of Graphs

| Directed | Undirected |
|-----------|------------|
| Edges have direction | Edges have no direction |
| Airline Routes | Friendship |

---

## Important Concepts

- Path → No repeated vertices.
- Walk → Repeated vertices allowed.
- Reachability → Existence of a path.
- Connected Graph → Every vertex reachable.

---

## Major Graph Problems

| Problem | Goal | Typical Application |
|---------|------|---------------------|
| Graph Colouring | Colour adjacent vertices differently | Timetabling, Register Allocation |
| Vertex Cover | Cover every edge with minimum vertices | CCTV Placement |
| Independent Set | Select maximum non-adjacent vertices | Event Scheduling |
| Matching | Pair vertices without conflicts | Project Allocation |

---

## Four Colour Theorem

- Applies only to **planar graphs**.
- Every planar graph can be coloured with **at most four colours**.

---