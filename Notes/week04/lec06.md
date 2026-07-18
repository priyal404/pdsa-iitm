# Lecture 6: Introduction to Directed Acyclic Graphs (DAGs)

> **Course:** Programming Data Structures and Algorithms using Python
>
> **Week:** 4
>
> **Lecture:** 6

---

# Introduction / Overview

In the previous lecture, we learned how **Breadth First Search (BFS)** and **Depth First Search (DFS)** can detect cycles in graphs.

- In **undirected graphs**, cycles can be detected by identifying **non-tree edges**.
- In **directed graphs**, DFS classifies edges using **pre/post numbering**, and **back edges** indicate cycles.

This lecture introduces an important class of directed graphs known as **Directed Acyclic Graphs (DAGs)**.

DAGs arise naturally whenever there are **tasks with dependencies**, where certain tasks must be completed before others. Examples include:

- Construction projects
- Software compilation
- Course prerequisite planning
- Manufacturing processes
- Project scheduling

Two fundamental computational problems on DAGs are introduced:

1. **Topological Sorting** – finding a valid order of execution.
2. **Longest Path** – determining the minimum completion time under dependency constraints.

---

# Directed Acyclic Graph (DAG)

A **Directed Acyclic Graph (DAG)** is a directed graph that contains **no directed cycles**.

This means:

- Every edge has a direction.
- Following the direction of edges, it is impossible to return to the starting vertex.

---

## Why "Acyclic"?

Suppose we have two tasks:

- A
- B

If we specify

```
A → B
```

it means

> Complete **A before B**.

If we also specify

```
B → A
```

then the requirements become impossible.

```
A before B
B before A
```

Neither task can begin.

Such dependency graphs are therefore invalid.

Hence, **dependency graphs must not contain cycles**.

---

# Motivating Example: Setting Up a New Office

Consider a startup moving into a new office.

Several tasks must be completed before employees can occupy the office.

Possible tasks include:

- Lay electrical conduits
- Lay telecom conduits
- Tile the floor
- Plaster the walls
- Paint the walls
- Electrical wiring
- Telecom cabling
- Electrical fittings

These tasks cannot be performed in arbitrary order.

---

## Dependency Constraints

Some natural constraints are:

- Conduits must be laid before tiling.
- Conduits must be laid before plastering.
- Plastering must finish before painting.
- Tiling should finish before painting.
- Painting should finish before wiring.
- Painting should finish before cabling.
- Wiring must finish before electrical fittings.

These dependencies are naturally represented using a directed graph.

---

## Graph Representation

Each task becomes a **vertex**.

Each dependency becomes a **directed edge**.

Example:

```
Electrical Conduits ──► Tiling
                     └──► Plastering

Telecom Conduits ─────► Tiling
                     └──► Plastering

Tiling ───────────────► Painting

Plastering ───────────► Painting

Painting ─────────────► Wiring

Painting ─────────────► Cabling

Wiring ───────────────► Electrical Fittings
```

The arrows indicate mandatory ordering constraints.

---

# Why Cycles Are Not Allowed

Suppose the graph contained

```
A → B
B → C
C → A
```

This would imply

- A before B
- B before C
- C before A

No valid execution order exists.

Hence,

> **A task dependency graph must always be acyclic.**

---

# Multiple Valid Execution Orders

An important property of DAGs is that there is usually **more than one valid schedule**.

Example 1

```
Electrical Conduits
Telecom Conduits
Tiling
Plastering
Painting
Wiring
Cabling
Electrical Fittings
```

---

Example 2

```
Telecom Conduits
Electrical Conduits
Plastering
Tiling
Painting
Wiring
Electrical Fittings
Cabling
```

Both satisfy all dependencies.

The exact order may depend upon:

- Worker availability
- Resource allocation
- Optimization objectives
- Scheduling constraints

---

# DAG as a Model for Task Scheduling

A DAG provides a mathematical representation of scheduling problems.

| Graph Component | Represents |
|-----------------|------------|
| Vertex | Task |
| Directed Edge | Dependency |
| Source Vertex | Task with no prerequisites |
| Sink Vertex | Final task |
| Path | Sequence of dependent tasks |

Thus,

```
Task A
   ↓
Task B
   ↓
Task C
```

means

```
A must finish
      ↓
B may start
      ↓
C may start
```

---

# Topological Sorting

The central scheduling problem is:

> Find an ordering of tasks that satisfies every dependency.

This ordering is called a **Topological Ordering**.

The process of computing such an ordering is called:

> **Topological Sorting**

---

## Definition

A topological ordering is a sequence of vertices such that

For every edge

```
u → v
```

vertex **u appears before v** in the ordering.

---

### Valid Example

```
A → B
A → C
B → D
C → D
```

Valid ordering:

```
A
B
C
D
```

Another valid ordering:

```
A
C
B
D
```

Both satisfy every dependency.

---

## Invalid Ordering

```
B
A
C
D
```

This violates

```
A → B
```

Therefore it is **not** a topological ordering.

---

# Why Multiple Topological Orders Exist

Many tasks are independent.

Example:

```
Electrical Conduits

Telecom Conduits
```

Neither depends on the other.

Hence either can be executed first.

Only dependency constraints matter.

Independent tasks may appear in any order.

---

# Longest Path in a DAG

Another important question is:

> What is the **minimum possible completion time**?

Assume:

- Unlimited workers are available.
- Every task takes one day.
- Dependencies cannot be violated.

---

## Example

```
Conduits
      ↓
Plastering
      ↓
Painting
      ↓
Wiring
      ↓
Electrical Fittings
```

This chain has

```
5 tasks
```

Even with unlimited workers,

each task depends on the previous one.

Therefore

```
Minimum completion time = 5 days
```

---

## Why the Longest Path Matters

Parallel tasks can execute simultaneously.

Example

```
        Painting
       /        \
 Wiring        Cabling
```

Both can happen together.

However,

any chain of dependencies cannot be shortened.

Therefore,

> The **longest dependency chain** determines the minimum completion time.

This longest dependency chain is called the **Longest Path**.

---

# Applications of DAGs

## 1. Project Scheduling

Examples:

- Building construction
- Office setup
- Factory installation

Each activity depends on previous activities.

---

## 2. Academic Course Planning

Courses often have prerequisites.

Example

```
Programming

     ↓

Data Structures

     ↓

Algorithms
```

A student cannot study Algorithms before Data Structures.

Topological sorting provides a valid semester-wise order.

The longest path determines the minimum number of semesters required.

---

## 3. Cooking and Food Preparation

Different cooking tasks may execute simultaneously.

Example:

```
Marinate Chicken

       ↓

Cook Chicken
```

Meanwhile,

```
Chop Vegetables
```

can happen independently.

A DAG helps optimize preparation time.

---

## 4. Construction Projects

Construction naturally follows dependency chains.

Example:

```
Foundation

      ↓

Columns

      ↓

Slabs

      ↓

Walls

      ↓

Painting
```

Removing dependencies is impossible.

The DAG determines the earliest completion schedule.

---

## 5. Software Build Systems

Large software projects consist of modules.

Example:

```
Library A

     ↓

Library B

     ↓

Application
```

Compilation follows dependency order.

Build systems perform topological sorting before compilation.

---

# Why DAGs Are Important

Although acyclic graphs appear simpler than cyclic graphs,

they solve numerous real-world scheduling problems.

Their importance comes from representing:

- Dependencies
- Execution order
- Parallelism
- Earliest completion time

Many optimization algorithms operate specifically on DAGs because the absence of cycles simplifies computation.

---

# Relationship with Previous Lecture

The previous lecture showed how DFS detects cycles.

This lecture builds upon that result.

Workflow:

```
Graph

   │

Check for Cycles

   │

No Cycles

   ▼

Directed Acyclic Graph (DAG)

   │

Topological Sort

   │

Longest Path

   ▼

Scheduling Problems
```

Thus,

cycle detection is often the first step before applying DAG algorithms.

---

# Key Takeaways

- A **Directed Acyclic Graph (DAG)** is a directed graph with no directed cycles.
- DAGs naturally model **tasks and dependency constraints**.
- A cycle in a dependency graph represents an impossible scheduling situation.
- **Topological Sorting** produces a valid order of task execution.
- Multiple topological orders may exist because independent tasks can be executed in any order.
- The **Longest Path** determines the minimum completion time under dependency constraints.
- DAGs are widely used in project management, software builds, course planning, cooking workflows, and construction scheduling.

---

# Important Formulae

No major mathematical formulae were introduced.

Important concepts:

- DAG = Directed graph with **no cycles**
- Topological Ordering:

```
For every edge

u → v

u must appear before v.
```

- Minimum completion time (unit task duration):

```
Length of Longest Path
```

---

# GATE / Interview Focus

## Must Remember

- DAGs contain **no directed cycles**.
- Dependency graphs must always be DAGs.
- Topological sorting exists **only for DAGs**.
- Multiple valid topological orders may exist.
- Longest path in a DAG represents the critical dependency chain.
- Cycle detection is often performed before topological sorting.
- Vertices represent tasks, while directed edges represent prerequisites or dependencies.

---

# Common GATE Questions

### Q1. What is a Directed Acyclic Graph (DAG)?

**Answer:**

A directed graph that contains no directed cycles.

---

### Q2. What does a directed edge represent in a task dependency graph?

**Answer:**

A precedence constraint, meaning one task must be completed before another.

---

### Q3. What is Topological Sorting?

**Answer:**

An ordering of vertices such that every directed edge goes from an earlier vertex to a later vertex in the sequence.

---

### Q4. Why can multiple topological orders exist?

**Answer:**

Independent tasks have no ordering constraints and may appear in any relative order.

---

### Q5. What determines the minimum completion time of a DAG with unit-duration tasks?

**Answer:**

The length of the longest dependency path (critical path).

---

# Flashcards

**Q:** What does DAG stand for?

**A:** Directed Acyclic Graph.

---

**Q:** What does a vertex represent in a scheduling DAG?

**A:** A task.

---

**Q:** What does a directed edge represent?

**A:** A dependency or prerequisite.

---

**Q:** What happens if a dependency graph contains a cycle?

**A:** No valid execution order exists.

---

**Q:** What is Topological Sorting?

**A:** Finding a valid ordering of tasks that satisfies all dependencies.

---

**Q:** Can a DAG have multiple valid topological orders?

**A:** Yes.

---

**Q:** What determines the minimum completion time in a DAG?

**A:** The longest dependency path.

---

# Practice MCQs

### Q1. A Directed Acyclic Graph (DAG) is:

A. An undirected graph

B. A directed graph with cycles

C. A directed graph without cycles

D. A complete graph

**Answer:** C

---

### Q2. Topological sorting is possible only for:

A. Complete graphs

B. Trees

C. DAGs

D. Weighted graphs

**Answer:** C

---

### Q3. In a task dependency graph, a directed edge from A to B means:

A. B must be completed before A

B. A and B are independent

C. A must be completed before B

D. A and B execute simultaneously

**Answer:** C

---

### Q4. Multiple topological orderings are possible because:

A. Graphs contain cycles

B. Independent tasks may be reordered

C. Every vertex has multiple parents

D. DFS always gives different answers

**Answer:** B

---

### Q5. The minimum completion time for unit-duration tasks is determined by:

A. Number of vertices

B. Number of edges

C. Longest dependency path

D. Shortest path

**Answer:** C

---

# One-Page Revision

- **DAG = Directed graph with no cycles.**
- DAGs model **tasks and dependencies**.
- Vertices represent **tasks**.
- Directed edges represent **prerequisite relationships**.
- Cycles imply impossible scheduling constraints.
- **Topological Sorting** finds a valid execution order.
- Multiple topological orders may exist.
- Independent tasks can execute in any relative order.
- The **Longest Path** is the critical dependency chain.
- The longest path determines the minimum completion time when tasks have equal duration.
- Common applications include project scheduling, course planning, software builds, cooking workflows, and construction management.