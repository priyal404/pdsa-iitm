## Graded Assignment 2

1)

```
def fun(n):
    total = 0
    for i in range(n):
        total += i

    k = 0
    for i in range(n):
        for j in range(n):
            k += (i * j)
            for l in range(5):
                k += 1

    for i in range(1000):
        total -= 1

    return total + k
```

What is the time complexity of the given function **fun**?

1. *O(n)*
1. *O(n^2)*
1. *O(n^3)*
1. *O(1)*

**Ans:- 2. O(n^2)**

---

2)
```
def func(n):
    s = 0
    if n <= 0:
        return 0
    for i in range(n):
        j = 0
        while j * j < n:
            s += j
            j += 1
    return s
```

What is the time complexity of the given function **fun*?

1. *O(n)*
1. *O(n^2)*
1. *O(n log n)*
1. *O(n sqrt(n))*

**Ans:- 4. *O(n sqrt(n))***

---

3) Let *T(best)(n)*, *T(avg)(n)*, and *T(worst)(n)* be the best-case, and worst-case running times of an algorithm, respectively, executed on an input of size *n*.

Which of the following statement(s) is/are always true regarding these running times? [MSQ]

1. *T(best)(n) = O(T(avg)(n))*
1. *T(worst)(n) = Ω(T(avg(n))*
1. if *T(best)(n) = Θ(n^2) and T(worst)(n) = Θ(n^2), then T(avg)(n) = Θ (n^2)*
1. T(avg)(n) = O(T(best)(n))*

**Ans:- 1, 2, 3.**

1. *T(best)(n) = O(T(avg)(n))*
1. *T(worst)(n) = Ω(T(avg(n))*
1. if *T(best)(n) = Θ(n^2) and T(worst)(n) = Θ(n^2), then T(avg)(n) = Θ (n^2)*

---

4) Consider the below function for selection sort algorithm.

```
def selectionsort(L):
    n = len(L)
    if n < 1:
        return(L)

    for i in range(n-1):
        minpos = i
        for j in range(i+1, n):
            if L[j] < L[minpos]:
                minpos = j

        (L[i], L[minpos]) = (L[minpos], L[i])  # Swap Operation

    return(L)
```

Consider the list L = [5, 2, 8, 2, 4] . If this list is sorted using the provided selectionsort algorithm, how many effective swaps will be performed? (An effective swap is counted only when minpos != i at the moment of the swap). (Type: Numeric)

**Ans:- 3**

---

5) 

```
def insertionsort(L):
    n = len(L)
    if n < 1:
        return(L)

    for i in range(n):
        j = i
        while(j > 0 and L[j] < L[j - 1]):
            (L[j], L[j - 1]) = (L[j - 1], L[j])
            j = j - 1

    return(L)
```

Which of the following statement(s) is/are correct with regard to the given insertion sort? [MSQ]

1. The sort is stable and it does not sort in-place
1. The sort is unstable and it sorts in-place
1. The sort is stable and it sorts in-place
1. After m iterations of the for-loop, the first m elements in the list are in sorted order
1. After m iterations of the for-loop, the first m elements in the list are the m smallest elements of the list

**Ans:- 1, 4.**

3) The sort is stable and it sorts in-place
4. After m iterations of the for-loop, the first m elements in the list are in sorted order

---

6) You are implementing binary search on a sorted array that may contain duplicate values of the target element X. You need to find the index of the last occurrence of X . If an instance of X is found at L[mid] , how should the search proceed to find the last possible occurrence?

1. Store mid as a potential answer and continue searching in the left subarray by setting high = mid - 1 .
1. Immediately return mid , as binary search on a sorted array with duplicates will always find the last occurrence if multiple exist.
1. Store mid as a potential answer and continue searching in the right subarray by setting low = mid + 1 .
1. Discard mid and search both the left ( high = mid - 1 ) and right ( low = mid + 1 ) subarrays recursively.

**Ans:- 3. Store mid as a potential answer and continue searching in the right subarray by setting low = mid + 1 .**

---

7) A school wants to maintain a database of its students. Each student has a unique id and it is stored along with other details. Adding a new student with a unique id, searching for a student using their id, and removal of students are the frequent operations performed on the database. From the options given below, choose the most efficient technique to store the data.

1. Maintain a sorted list with id. Whenever a new student is added, append the student details at the end, and sort the entire list using selection sort.
1. Maintain a sorted list with id. Whenever a new student is added, append the student details at the end, and sort the entire list using insertion sort.
1. Maintain a sorted list with id. Whenever a new student is added, append the student details at the end, and sort the entire list using merge sort.
1. Maintain a sorted list with id. Whenever a new student is added, insert the student details into the respective positio**

**Ans:- 4. Maintain a sorted list with id. Whenever a new student is added, insert the student details into the respective position in the sorted list by id.**

---

8)

```
def tsearch(L, x):
    global c
    c += 1
    n = len(L)

    if n == 0:
        return False

    if L[n // 3] == x:
        return True

    if L[2 * n // 3] == x:
        return True

    if x < L[n // 3]:
        return tsearch(L[:n // 3], x)

    elif x > L[2 * n // 3]:
        return tsearch(L[2 * n // 3:], x)

    else:
        return tsearch(L[n // 3 : 2 * n // 3], x)
```

Choose the order of complexity of the search function tsearch.

1. *O(n)*
1. *O(log n / n^2)*
1. *O(log n)*
1. *O(log n / n*

**Ans:- 3. *O(log n)***

---

9)  Arrange the following functions in increasing order of asymptotic complexity.

*f1(n) = 3n + log n*
*f2(n) =  (log n)^2*
*f3(n) =  log(log n)*
*f4(n) =  100 log n*
*f5(n) = 3n log n*

1. *f3(n), f4(n), f2(n), f1(n), f5(n)*
1. *f3(n), f2(n), f1(n), f5(n), f4(n)*
1. *f2(n), f3(n), f4(n), f5(n), f1(n)*
1. *f2(n), f3(n), f4(n), f1(n), f5(n)*

**Feedback:** f3 < f4 < f2 < f1 < f5

**Ans:- 1. *f3(n), f4(n), f2(n), f1(n), f5(n)***

---

10) Consider the following functions:

*f(n)  = 2^(log n) log n*
*g(n) = n log log n*
*h(n) = n(log n)^2*

Which of the following options is correct?

*f(n) = O(g(n)), g(n) = O(h(n))*
*f(n) = Ω(g(n)), g(n) = O(h(n))*
*g(n) = O(f(n)), h(n) = O(f(n))*
*g(n) = O(f(n)), h(n) = O(f(n))*

**Ans:- 2. *f(n) = Ω(g(n)), g(n) = O(h(n))***

---

11) Given the following sorted list:

[16, 53, 59, 81, 94, 99, 121, 150, 162, 170]

If we use binary search algorithm to search the element 99 in the list, then which of the following option corresponds to the correct sequence of comparison done in this process?

Note: Assume here binary search will compute the midpoint by using (first index + last index) // 2

1. 94, 99
1. 16, 99
1. 94, 150, 121, 99
1. 94, 150, 99
1. None of the above

**Ans:- 94, 150, 99**

---

12) Consider the following input list:

[38, 28, 43, 22, 112, 33, 39]

What will be the number of swaps that the following **insertion sort** will make to sort this given list? (Type: Numeric)

```
def insertionsort(L):
    n = len(L)
    if n < 1:
        return(L)
    for i in range(n):
        j = i
        while(j > 0 and L[j] < L[j-1]):
            (L[j], L[j-1]) = (L[j-1], L[j])
            j = j-1
    return(L)
```

**Ans:- 9**

---

13) We have an input list of two-dimensional points [(8,1), (7,5), (6, 1), (2, 5), (5, 2), (9, 0)]. We sort these in ascending order by the second coordinate. Which of the following corresponds to a **stable sort** of this input?

1. [(9, 0), (6, 1), (8, 1), (5, 2), (7, 5), (2, 5)]
1. [(9, 0), (8, 1), (6, 1), (5, 2), (7, 5), (2, 5)]
1. [(9, 0), (8, 1), (6, 1), (5, 2), (2, 5), (7, 5)]
1. [(9, 0), (6, 1), (8, 1), (5, 2), (2, 5), (7, 5)]

**Ans:- 2. [(9, 0), (8, 1), (6, 1), (5, 2), (7, 5), (2, 5)]**

---

14) Consider the following implementation for merge two sorted list and return one sorted merged list: (Type: Numeric)

```
def merge(A, B): # Merge two sorted list A and B
    (m,n) = (len(A), len(B))
    (C,i,j) = ([],0,0)
    #Case 1 :- when both lists A and B have elements for comparing

    while i < m and j < n:
        if A[i] <= B[j]: #Compare the elements
            C.append(A[i])
            i += 1
        else:
            C.append(B[j])
            j += 1
    #Case 2 :- If list B is over, shift all elements of A to C
    while i < m:
        C.append(A[i])
        i += 1
    
    #Case 3 :- If list A is over, shift all elements of B to C
    while j < n:
        C.append(B[j])
        j += 1
    # Return sorted merged list
    return C
```

**Ans:- 14**