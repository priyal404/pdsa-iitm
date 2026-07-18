# Lecture 08: Implementation of Dictionaries in Python

> **Course:** Programming, Data Structures and Algorithms using Python
>
> **Week:** 3
>
> **Lecture:** 8

---

# Lecture Notes

## Overview

In the previous lecture, we studied how Python implements **lists** using dynamic arrays. In this lecture, we move on to another important built-in data structure: **dictionaries**.

A dictionary stores information as **key-value pairs**, allowing values to be accessed directly using meaningful keys instead of numeric indices.

The lecture explains how Python dictionaries achieve fast lookups using **hash tables**, the role of **hash functions**, and how **collisions** are handled.

---

## Lists vs Dictionaries

Lists and dictionaries both store collections of data, but they differ in how elements are accessed.

### Lists

A list stores elements in order.

Each element is identified by its **position (index)**.

Example:

```python
L = [10, 20, 30]

print(L[1])
```

Output

```
20
```

The index ranges from

```
0 to n-1
```

where **n** is the length of the list.

---

### Dictionaries

A dictionary stores **key-value pairs**.

Instead of using positions,

we use a **key** to retrieve its associated value.

Example:

```python
marks = {
    "Alice": 92,
    "Bob": 85,
    "Charlie": 90
}

print(marks["Bob"])
```

Output

```
85
```

Here,

```
Key → "Bob"

Value → 85
```

---

## Why Do We Need Dictionaries?

Suppose we want to store student marks.

One approach would be:

```
Roll Number

↓

Array Index

↓

Marks
```

However,

if we want to search using names,

```
"Alice"

↓

92
```

we do **not** want to first convert every name into an index.

Instead,

we would like to directly write

```python
marks["Alice"]
```

and immediately obtain

```
92
```

This is called a **key-value store**.

---

## Requirement: Fast Access

Even though dictionary keys are arbitrary values,

we still want lookup to behave like array indexing.

That means

```
marks[key]
```

should take approximately the **same amount of time** regardless of which key is used.

This property is known as **constant-time lookup** (on average).

The challenge is that arrays only support integer indices.

Therefore,

we need a way to convert arbitrary keys into valid array positions.

---

## The Need for a Hash Function

Arrays use indices such as

```
0
1
2
3
...
n−1
```

Dictionary keys, however, can be

- Strings
- Numbers
- Tuples
- Other immutable objects

Therefore,

we require a function that converts any valid key into an integer index.

This function is called a **hash function**.

```
Key

↓

Hash Function

↓

Array Index
```

Example:

```
"Alice"

↓

Hash Function

↓

17
```

Now,

instead of searching through every key,

Python directly jumps to

```
Array[17]
```

---

## What Is a Hash Function?

A **hash function** maps a key from a very large set of possible values into a fixed range of integers.

Conceptually,

```
h(key)

↓

0 ... n−1
```

where

```
n
```

is the size of the underlying hash table.

Examples:

```
"Alice"

↓

23
```

```
"Bob"

↓

104
```

```
"Charlie"

↓

58
```

Each key is converted into an array position where its value can be stored.

This allows dictionaries to achieve very fast lookups.

---

## Why Collisions Are Unavoidable

The number of possible keys is enormous.

For example,

there are millions of possible names,

strings,

or combinations of characters.

However,

our hash table contains only a limited number of positions.

Therefore,

different keys may produce the same hash value.

Example:

```
"Alice"

↓

15
```

```
"David"

↓

15
```

Both keys map to the same array position.

This situation is called a **collision**.

---

## Collision

A collision occurs when

```
h(k₁) = h(k₂)

where

k₁ ≠ k₂
```

That is,

two different keys receive the same hash value.

Collisions cannot be completely avoided because

```
Large Set of Keys

↓

Small Range of Array Indices
```

Eventually,

multiple keys must share the same position.

The objective is **not** to eliminate collisions,

but to make them **rare** and distribute them as evenly as possible.

---

## Characteristics of a Good Hash Function

A good hash function should:

- Convert arbitrary keys into valid array indices.
- Spread keys uniformly across the table.
- Minimize collisions.
- Produce approximately random-looking outputs.
- Allow constant-time computation.

If many keys map to the same location,

dictionary performance decreases.

Therefore,

the quality of the hash function has a significant impact on the efficiency of dictionaries.

---

## SHA-256: An Example of a Hash Function

One widely used real-world hash function is **SHA-256**.

SHA stands for **Secure Hash Algorithm**,

and **256** refers to the fact that the output consists of **256 bits**.

```
Input (Any Size)

↓

SHA-256

↓

256-bit Hash Value
```

The input can be

- A string
- A document
- An image
- A video
- An entire file

Regardless of the input size,

the output is always a fixed-length 256-bit value.

---

## Why Is SHA-256 Important?

SHA-256 is widely used in

- Cryptography
- Digital signatures
- Password verification
- Blockchain
- Cloud storage systems

One important property is that it is **extremely unlikely** for two different inputs to produce the same hash value.

Although collisions are theoretically possible,

they are so rare that they are practically ignored.

---

## Example: Cloud Storage

Suppose you upload a large file to a cloud storage service.

Instead of immediately copying the file,

the service first computes its SHA-256 hash.

```
Large File

↓

SHA-256

↓

Hash Value
```

If another file with the **same hash** already exists,

the storage system may simply create another reference to the existing file instead of storing a duplicate copy.

This saves

- Storage space
- Upload time
- Network bandwidth

---

## Why Does This Work?

For this optimization to be safe,

the hash function must satisfy an important property.

Different files should almost never produce the same hash value.

If two different files produced identical hashes,

the storage system might incorrectly assume they are the same file.

Because SHA-256 has an enormous output space,

such collisions are considered practically impossible.

---

## Hash Tables

A **hash table** combines

- An array
- A hash function

The array stores the data,

while the hash function determines where each key should be placed.

```
Key

↓

Hash Function

↓

Array Index

↓

Stored Value
```

For example,

```
"Alice"

↓

Hash Function

↓

12

↓

marks[12] = 92
```

Thus,

instead of searching through every stored key,

Python directly jumps to the computed array position.

---

## Storing a Key-Value Pair

Suppose we execute

```python
marks["Alice"] = 92
```

The process is:

```
"Alice"

↓

Hash Function

↓

12

↓

Store 92 at Array[12]
```

Later,

when we retrieve

```python
marks["Alice"]
```

Python performs the same hash computation.

```
"Alice"

↓

Hash Function

↓

12

↓

Return Value
```

Since the same key always produces the same hash value,

Python immediately finds the stored value.

---

## The Collision Problem

Suppose we already have

```
"Alice"

↓

12
```

Now,

another key also produces

```
"David"

↓

12
```

Both keys want to occupy

```
Array[12]
```

Only one value can occupy that location directly.

This creates a **collision**.

Therefore,

Python must use a strategy to store both key-value pairs without losing either one.

---

## Methods of Handling Collisions

Two standard techniques are used:

1. **Open Addressing (Closed Hashing)**
2. **Open Hashing (Separate Chaining)**

Both aim to store every key even when collisions occur.

The difference lies in **where the colliding element is stored**.

---