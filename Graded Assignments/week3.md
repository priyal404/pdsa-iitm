## Graded Assignment 3

1) The recurrence relation *T(n) = T(k) + T(n - k - 1) + O(n)* describes the running time of Quicksort, where *k* is the number of elements smaller than the pivot after partitioning. Which scenario leads to the worst-case time complexity of Quicksort, and what does *k* approximate in this case?

1. When the pivot consistently divides the array into two nearly equal halves; *k ≈ n/2*.
1. When the pivot selected is always the smallest or largest element in the current subarray; *k ≈ 0* or *k ≈ n - 1*.
1. When the input array is already sorted, and the pivot is chosen as the middle element; *k ≈ n/2*.
1. The partitioning step itself takes *O(n^2)* time due to poor pivot choice; *k* is irrelevant in this case.

**Ans:- 2. When the pivot selected is always the smallest or largest element in the current subarray; *k ≈ 0* or *k ≈ n - 1*.**

---

2) Which of the following statements accurately describes the **stability** and **in-place** nature of the standard Quicksort algorithm?

1. Quicksort is stable and sorts in-place.
1. Quicksort is not stable but sorts in-place.
1. Quicksort is stable but does not sort in-place.
1. Quicksort is not stable and does not sort in-place.

**Feedback:**

**Stability**: Standard Quicksort is **not stable**. During the partitioning process, elements with equal values might have their relative order changed. For instance, if you are partitioning an array and encounter elements equal to the pivot, their original order relative to other equal elements (or even elements equal to the pivot that are on the other side of the pivot's final position) is not guaranteed to be preserved.

**In-place**: Quicksort is generally considered an **in-place** sorting algorithm. This means it sorts the elements within the original array, requiring only a small, constant amount of additional memory (O(1)) for variables during the partitioning step.

**Ans:- 2. Quicksort is not stable but sorts in-place.**

---

3) You are given a pointer p to an arbitrary node in a **singly linked list**. This node p is guranteed not to be the tail node. You need to effectively "delete" the node p (i.e., remove the value it holds from the sequence) but you do **not** have acess to the head pointer or any pointer to the node preceding p. Which of the following sequence of operations correctly and most efficiently achieves this?

1. Copy p.data into p.next.data. Then set p.next = p.next.next.
1. Copy p.data into p.next.data. Then set p.next = p.next.next.
1. Create a temporary pointer temp = p.next. Copy temp.data to p.data. Set p.next = temp.next.
1. It's impossible to delete node p or effectively remove its value from the list structure under these constraints, as modifying the preceding node's next pointer is essential.

**Feedback:** This is a classic "trick" for deleting a node in a singly linked list when you don't have a pointer to its predecessor. The method doesn't truly delete the node p itself (in terms of memory deallocation of p), but rather it overwrites p's data with the data of the next node and then bypasses/deletes that next node.

temp = p.next: Store a pointer to the node following p.Since p is not the tail, p.next is valid.
p.data = temp.data (or p.data = p.next.data): Copy the data from the next node into the current node p. .
p.next = temp.next (or p.next = p.next.next): Make p point to the node after its original successor, effectively bypassing the original successor.
free(temp) (or language equivalent): Deallocate the memory of the original successor node, which is no longer needed.
(B) is incorrect because you cannot efficiently "work backward" in a singly linked list.
(C)is incorrect because it copies p's data forward, which doesn't achieve deletion of p's original value, and it incorrectly modifies p.next.data before linking.
(D) is incorrect because option (A) provides a valid method to achieve the effective deletion of the value at node p.

**Ans:- 3. Create a temporary pointer temp = p.next. Copy temp.data to p.data. Set p.next = temp.next.**

---

4) The following Python function mystery_operation takes the head of a singly linked list as input. What does this function effectively do to the list?

```
class Node:
	def __init__(self, data):
		self.data = data
		self.next = None

def mystery_operation(head: Node) -> Node:
	if not head or not head.next:
		return head

	prev = None
	current = head
	while current:
		next_node = current.next 	# Store next node
		current.next = prev 			# Reverse current node's pointer
		prev = current 				# Move prev one step forward
		current = next_node 		# Move current one step forward
	return prev 					# New head
```

1. It deletes all duplicate nodes from the linked list.
1. It reverses the linked list in-place.
1. It sorts the linked list in ascending order.
1. It creates a circular linked list by connecting the tail to the head.

**Feedback:**

**Explanation**: This function implements the standard iterative algorithm to **reverse a singly linked list inplace**.
prev keeps track of the previous node (initially None as it will become the new tail's next).
current iterates through the list.
next_node temporarily stores the original next node before current.next is modified.
current.next = prev reverses the pointer of the current node to pointto its prev ious node.
prev = current and current = next_node advance the prev and current pointers. When current becomes None, prev will be pointing to the last node of the original list, which is now the new head of the reversed list. 

**Ans:- 2. It reverses the linked list in-place.**

---

5) Start with an empty stack S and an empty queue Q. The following sequence of operations is performed in the given order:

	1.  Q.enqueue(8)
	2.  Q.enqueue(3)
	3.  S.push(Q.dequeue())
	4.  S.push(12)
	5.  Q.enqueue(S.pop())
	6.  Q.enqueue(Q.dequeue())
	7.  S.push(7)
	8.  S.push(Q.dequeue())
	9.  Q.enqueue(S.pop())
	10. S.push(Q.dequeue())
	11. Q.enqueue(19)
	12. S.push(S.pop())

After all these operations are completed, what are the contents of stack S (from bottom to top) and queue Q (from front to rear)? 

1. Stack S: [8, 7, 12] Queue Q: [19, 3] 
1. Stack S: [8, 12, 7] Queue Q: [3, 19]
1. Stack S: [8, 3, 7] Queue Q: [19, 12] 
1. Stack S: [8, 7, 3] Queue Q: [12, 19] 

**Feedback:**

Let's trace the state of stack S (bottom element shown on the left, top on the right) and queue Q (front element shown on the left, rear on the right) after each operation.

**Initial**: S: [ ] Q: [ ]
	1. Q.enqueue(8) S: [ ] Q: [8]
	2. Q.enqueue(3) S: [ ] Q: [8, 3]
	3. S.push(Q.dequeue()) (Q.dequeue() returns 8, Q becomes [3] .S.push(8)) S: [8] Q: [3]
	4. S.push(12) S: [8, 12] Q: [3]
	5. Q.enqueue(S.pop()) (S.pop()returns 12, S becomes [8].Q.enqueue(12)) S: [8] Q: [3, 12]
	6. Q.enqueue(Q.dequeue()) (Q.dequeue() returns 3, Q becomes [12] . Q.enqueue(3)) S: [8] Q: [12, 3]
	7. S.push(7) S: [8, 7] Q: [12, 3]
	8. S.push(Q.dequeue()) (Q.dequeue() returns 12, Q becomes [3].S.push(12)) S: [8, 7, 12] Q: [3]
	9. Q.enqueue(S.pop()) (S.pop()returns 12, S becomes [8, 7].Q.enqueue(12)) S: [8, 7] Q: [3, 12]
	10. S.push(Q.dequeue()) (Q.dequeue() returns 3, Q becomes [12] .S.push(3)) S: [8, 7, 3] Q: [12]
	11. Q.enqueue(19) S: [8, 7, 3] Q: [12, 19]
	12. S.push(S.pop()) (S.pop() returns 3.S becomes [8, 7].S.push(3)) S: [8, 7, 3] Q: [12, 19] 

**Final States**:
Stack S (bottom to top): [8, 7, 3]
Queue Q (front to rear): [12, 19]

**Ans:- 4. Stack S: [8, 7, 3] Queue Q: [12, 19]**

---

6) **Linear probing** is an open addressing scheme in computer programming for resolving hash collisions in hash tables. Linear probing operates by taking the original hash index and adding successive values linearly until a free slot is found.

An example sequence of linear probing is:

*h(k)+0, h(k)+1, h(k)+2, h(k)+3 .... h(k)+m-1*

where *m* is a size of hash table, and *h(k)* is the hash function.

**Hash function**

Let *h(k) = k* mod m be a hash function that maps an element *k* to an integer in *[0, m−1]*, where *m* is the size of the table. Let the *ith* probe position for a value *k* be given by the function

*h'(k,i) = (h(k) + i) mod m*

The value of *i = 0, 1, . . ., m – 1*. So we start from *i = 0*, and increase this until we get a free block in hash table.

Consider inserting the keys *24, 36, 58, 65, 62, 79* into a hash table of size *m = 11* using linear probing, the primary hash function is *h(k) = k mod m*. What will be the hash table after inserting all keys in given order? Suppose initial hash table is: 
[None,None,None,None,None,None,None,None,None,None,None]

1. [None,None,24,36,58,None,79,62,None,65,None]
1. [None,None,24,36,58,79,None,62,None,None,65]
1. [None,24,None,36,58,79,None,62,None,None,65]
1. [None,None,24,36,58,None,79,62,None,None,65]

**Feedback:**

In linear probing, if the index generated by the hash function is already occupied, then we will check the next location by adding 1 until the free slot is not found. In the given question, initially, all slots in the hash table are empty.

24 mod 11 = 2 which is free. 24 will be stored at the 2nd index.

36 mod 11 = 3 which is free. 36 will be stored at the 3rd index.

58 mod 11 = 3 which is not free, then (3 + 1) mod 11 = 4 which is free. 58 will be stored at the 4rth index.

65 mod 11 = 10 which is free. 65 will be stored at the 10th index.

62 mod 11 = 7 which is free. 62 will be stored at the 7th index.

79 mod 11 = 2 which is not free then (2 + 1) mod 11 = 3 again slot is not free then (2 + 2) mod 11 = 4 again slot is not free then (2 + 3) mod 11 = 5 which is free 79 will be stored at the 5th index.

Hence, option (b) is correct.

**Ans:- 2. [None,None,24,36,58,79,None,62,None,None,65]**

---

7) In a quicksort algorithm, we choose the last element in the array as pivot for partitioning. For which of the following arrays will this algorithm exhibit the worst-case behavior? [MSQ]

1. [2, 3, 5, 7, 8, 13, 34, 46, 67]
1. [67, 46, 34, 13, 8, 7, 5, 3, 2]
1. [3, 5, 34, 2, 13, 67, 7, 46, 8]
1. [8, 46, 7, 67, 13, 2, 34, 5, 3]

**Feedback:**

If the input is sorted in any order then the partition procedure will divide the list into two sub list with 1 and n-1 elements each time so every time partition takes O(n) time and total n level is required to finish Quicksort algorithm. So this is the worst case for Quicksort algorithm. Hence, option (a) and (b) is correct input for the worst-case behavior of Quicksort.

**Ans:- 1, 2.**

1. [2, 3, 5, 7, 8, 13, 34, 46, 67]
1. [67, 46, 34, 13, 8, 7, 5, 3, 2]

---

8) In a linked list, what is the asymptotic worst-case running time for finding the size of the list?

1. *O(1)*
1. *O(log n)*
1. *O(n log n)*
1. *O(n)*

**Feedback:**

For finding the size of linked list, we have to traverse each element from starting. Hence, option (d) is correct.

**Ans:- 4. *O(n)***

---

9) For Quicksort on an input size n, where we always select the first element as pivot, how many partitioning levels required in worst-case and best-case, respectively?

1. *log n, n*
1. *log n, log n*
1. *n, log n*
1. *n, n*

**Feedback:**

In the worst case, the list will be divided into two sub list with 1 and n-1 elements, in that case, the number of partition levels will be n. And in the best case, the list will always divide into two equal sub-list, due to this, the number of partition levels will be logn

**Ans:- 3. *n, log n***

---

10) Consider two lists *L1* and *L2* both containing *n* integers. We need to find if lsits *L1* and *L2* are disjoint. Two lists are disjoint, if there is no integer common in both the lists.

For example,

1. *L1* = [5, 2, 7 , 1] and *L2* = [3, 5], these two lists are not disjoint as 5 is common in both lists.
1. *L1* = [2, 7, 1] and *L2* = [3, 5], these two lists are disjoint as there is no integer common in both.

Select the most efficient solution or solutions for this in terms of asymptotic running time complexity from the below list. [MSQ]

1. For every integer in L1 search if it is present in L2 or not.
1. Sort list L1, then for each integer i in L2, use binary search to find if i is present in L1 or not.
1. Sort both lists L1 and L2, then use merge like process to compare integers in both the lists.
1. Sort list L1, then for each integer i in L1 search if i is present in L2 or not.

**Ans:- 2, 3.**

2. Sort list L1, then for each integer i in L2, use binary search to find if i is present in L1 or not.
1. Sort both lists L1 and L2, then use merge like process to compare integers in both the lists.

---

11) What does the function operation(head) do? head is the first node of the linked list, where each node is an object of class Node , and the function returns True or False .

```
class Node:
    def __init__(self,data):
        self.data = data
        self.next = None
```

```
def operation(head):
    stack = []
    temp = head
    isoperation = True
    wile (temp != None):
        stack.append(temp.data)
        temp = temp.ext
    while (head != None):
        i = stack.pop()
        if head.data == i:
            isoperation = True
        else:
            isoperation = False
            break
        head = head.next
    return isoperation
```

1. Check if linked list contains loop or not.
1. Check if linked list is palindrome or not.
1. Search if a particular element is present in linked list.
1. Check if linked list is in sorted order.

**Feedback: By first while loop, we are adding all element of linked list in stack then in second while loop, we are traversing list from start and compare each element of list by popped element of stack. That means function operation checking whether the list is palindrome or not.**

**Ans:- 2. Check if linked list is palindrome or not.**

---

12) A hash table of size 8 (index 0 to 7) uses open addressing with hash function h(k) = k mod 8, and linear probing. The following elements are added into the hash table, which was intiially empty.

25,11,84,26,46 and 50

The key value 50 is stored at which index of the hash table? (Type: Numeric)

**Ans:- 5**

---

13) **Linear probing** is an open addressing scheme in computer programming for resolving hash collisions in hash tables. Linear probing takes the original hash index and increments the value by 1 until a free slot is found.

Consider the given hash table with hash function h(key) = key mod 5 which uses linear probing for solving collisions.

| Index | Key |
| --- | --- |
| 0 | 35 |
| 1 | 11 |
| 2 | 20 |
| 3 | 23 |
| 4 | 14 |

Which among the following options correspond to possible orders of insertion of values in the hash table?

1. 11, 23, 35, 20, 14
1. 14, 35, 23, 11, 20
1. 23, 35, 14, 20, 11
1. 23, 20, 35, 11, 14

**Ans:- 1, 2.**

1. 11, 23, 35, 20, 14
1. 14, 35, 23, 11, 20

---

14) Select the most appropriate data structure for the following applications.

| **Application** | **Data Structure** |
| --- | --- |
| 1. To implement undo/redo operation in the text editor | a. Array |
| 2. Matrix operations | b. Graph |
| 3. To implement printer spooler to store print request | c. Queue |
| 4. Facebook's Friend suggestion algorithm | d. Stack |

1. 1-d, 2-a, 3-c, 4-b
1. 1-d, 2-b, 3-c, 4-a
1. 1-d, 2-a, 3-d, 4-c
1. 1-a, 2-d, 3-c, 4-b

**Ans:- 1. 1-d, 2-a, 3-c, 4-b**

---

15)

```
class Node:
    def __init__(self,data):
        self.data = data
        self.next = None
```

Consider an implementation of a singly linked list, where each node is created using the given class Node . Suppose it has a head pointer that points to the first node of the linked list and a tail pointer that points to the last element of the linked list.

Suppose we want to perform the following operations on the given linked list:-

1. Insertion of the new node at the front of the linked list.
1. Insertion of the new node at the end of the linked list.
1. Deletion of the first node of the linked list.
1. Deletion of the last node of the linked list.

Which of the following option represents the correct complexity for each operation?

1. 1 - *O*(1),2 - *O*(n), 3 - *O*(1), 4 - *O*(1)
1. 1 - *O*(1),2 - *O*(1), 3 - *O*(1), 4 - *O*(1)
1. 1 - *O*(1),2 - *O*(n), 3 - *O*(1), 4 - *O*(n)
1. 1 - *O*(1),2 - *O*(1), 3 - *O*(1), 4 - *O*(n)

**Ans:- 4. 1 - *O*(1),2 - *O*(1), 3 - *O*(1), 4 - *O*(n)**