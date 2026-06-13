## Graded Assignment 6

1) Consider a list *L* with *k* distinct numbers and a heap *H* with size *n*. What is the nearest upper bound for checking if every number in *L* is present in the heap *H*?

1. *O(kN)*
1. *O(k log N)*
1. *O(N log k)*
1. *O(log N log k)*

**Ans:- *O(kN)***

---

**Use the below information for the Questions 2 to 7**

Identify the below arrays as min heap, max heap or none. Type *min* if it is a min heap, *max* if it is a max heap, *none* otherwise.

---

2)
| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|---|---|---|---|---|---|---|---|

1. min
1. max
1. none

**Ans:- 1. min**

---

3)
| 67 | 65 | 43 | 54 | 6 | 2 | 1 | 19 | 5 |
|---|---|---|---|---|---|---|---|---|

1. min
1. max
1. none

**Ans:- 2. max**

---

4)
| 88 | 77 | 66 | 55 | 44 | 33 | 22 | 11 |
|---|---|---|---|---|---|---|---|

1. min
1. max
1. none

**Ans:- 2. max**

---

5)
| 1 | 2 | 3 | 4 | 8 | 5 | 6 | 7 |
|---|---|---|---|---|---|---|---|

1. min
1. max
1. none

**Feedback: When we choose the element from the array in the same sequence and construct the heap, it will be min-heap.**

**Ans:- 1. min**

---

6)
| 4 | 1 | 2 | 3 | 5 | 6 | 7 | 8 |
|---|---|---|---|---|---|---|---|

1. min
1. max
1. none

**Ans:- none**

---

7) Which of the following will correctly represent the max-heap, after inserting elements 1, 2, 3, 5, 7, 6 and 4 in the given order, starting with an empty heap?

1.
| 7 | 5 | 6 | 1 | 3 | 2 | 4 |
|---|---|---|---|---|---|---|
2.
| 7 | 5 | 6 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|---|---|
3.
| 7 | 6 | 5 | 4 | 3 | 2 | 1 |
|---|---|---|---|---|---|---|

**Ans:- 1.**

| 7 | 5 | 6 | 1 | 3 | 2 | 4 |
|---|---|---|---|---|---|---|

---

8) What is the nearest worst case upper bound to search for an element in a heap and in a binary search tree, respectively? Consider that the total number of elements are *n* and the binary search tree is balanced(in the form of a complete binary tree).

1. *O(log n), O(log n)*
1. *O(n), O(n)*
1. *O(n), O(log n)*
1. *O(log n), O(n)*

**Ans:- 3. *O(n), O(log n)***

---

9)

```
def max_heapify(A,k):
    l = 2 * k + 1
    r = 2 * k + 2
    largest = k
    if l < len(A) and A[l] > A[k]:
        largest = 1
    if r < len(A) and A[r] > A[largest]:
        largest = r
    if largest == k:
        A[k], A[largest] = A[largest], A[k]
        max_heapify(A, k)
def build_max_heap(A):
    n = int((len(A)//2)-1)
    for k in range(n, -1, -1):
        max_heapify(A,k)
```

Above code is an incorrect implementation of **max_heap**. Which of the following lines of code if replaced for the given line numbers will correct the above code?

1.

```
if largest != k: #line 9
max_heapify(A, largest) #line 11
```

2)

```
max_heapify(A, largest) #line 11
```

3.

```
max_heapify(A, largest) #line 11
for k in range(n): #line 15
```

4)

```
max_heapify(A, largest) #line 11
for k in range(n, -1, 0): #line 15
```

**Ans:- 1.**

```
if largest != k: #line 9
max_heapify(A, largest) #line 11
```

---

10) Consider a max heap, represented as the array, `[40, 30, 18, 20, 15, 16, 17, 10, 4]`. Now consider that a value 25 is inserted into this heap. After insertion, the new heap will be

1. `[40, 30, 18, 20, 15, 16, 17, 10, 4, 25]`
1. `[40, 30, 18, 20, 25, 16, 17, 10, 4, 15]`
1. `[40, 30, 18, 20, 16, 25, 17, 10, 4, 15]`
1. `[40, 30, 18, 25, 20, 16, 17, 10, 4, 15]`

**Ans:- `[40, 30, 18, 20, 25, 16, 17, 10, 4, 15]`**

---

11) Pre-Order traversal of binary search tree is 15,10,12,11,20,18,16,19. Which one of the following is the post-order traversal of the binary search tree?

1. 10,11,12,15,18,16,19,20
1. 11,12,10,16,19,20,18,15
1. 11,12,10,16,19,18,20,15
1. 11,12,10,20,15,18,19,16

**Ans:- 3. 11,12,10,16,19,18,20,15**

---

12) What form of tree traversal does the function **traverse(root)** implement, where **root** is the root node of a binary search tree?

```
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None
    def traverse(root):
        if root == None:
            return
        traverse(root.left)
        traverse(root.right)
        print(root.data, end=' ')
```

1. Pre-order
1. Post-order
1. In-order
1. Breadth first traversal

**Ans:- 2. Post-order**

---

13) Consider a max-heap **H** with *n* elements and *h* height. What is the nearest upper bound to remove the maximum eleent from max-heap **H**? [MSQ]

1. *O(h)*
1. *O(n)*
1. *O(log n)*
1. *O(1)*

**Ans:- 1. *O(h)*, 2. *O(log n)***

---

14) The given code implements a priority queue using a sorted list. Which of the following is the correct implementation of **delete_max** operation of an element from the priority queue? Note that the higher the number, the higher it's priority ?

```
class priorityQueue:
    def __init__(self):
        self.que=[]
    def delete_max(self):
        largest = 0
        for i in range(len(self.que)):
            if self.queue[i] > self.queue[largest]:
                largest = i+1
        item = self.que[largest]
        del self.que[largest]
        return item
```

```
class priorityQueue:
    def __init__(self): 
        self.que=[]
    def delete_max(self):
        largest = 0
        for i in range(len(self.que)):
            if self.queue[i] <= self.queue[largest]:
                largest = i
        item = self.que[largest]
        del self.que[largest]
        return item
```

```
class priorityQueue:
    def __init__(self):
        self.que=[]
    def delete_max(self):
        largest = 0
        for i in range(0, len(self.que)):
            if self.queue[i] > self.queue[largest]:
                largest = i
        item = self.que[largest]
        del self.que[largest]
        return item
```

```
class priorityQueue:
    def __init__(self):
        self.que=[]
    def delete_max(self):
        largest = 0
        for i in range(len(self.que)):
            if self.queue[i] < self.queue[largest]:
                largest = i + 1
        item = self.que[largest]
        del self.que[largest]
        return item
```

**Ans:- 3**

```
class priorityQueue:
    def __init__(self):
        self.que=[]
    def delete_max(self):
        largest = 0
        for i in range(0, len(self.que)):
            if self.queue[i] > self.queue[largest]:
                largest = i
        item = self.que[largest]
        del self.que[largest]
        return item
```