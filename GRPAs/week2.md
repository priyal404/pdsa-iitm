# GrPA 1

## Question

Write a Python function ***combinationSort(strList)*** that takes a list of unique strings `strList` as an argument, where each string is a combination of a letter from `a` to `z` and a number from 0 to 99, the initial character in string being the letter. For example, `a23`, `d5`, `q99` are some strings in this format. This function should sorts the list and return two lists `(L1, L2)` in the order mentioned below.

`L1`: First list should contain all strings sorted in ascending order with respect to the first character only. All strings with same initial character should be in the same order as in the original list.

`L2`: In the list `L1` above, sort the strings starting with same character, in descending order with respect to the number formed by the remaining characters.

**Example:**
***Sample input 1:***
```
d34, g54, d12, b87, g1, c65, g40, d77
```

***Sample output 1:***
```
L1: b87, c65, d34, d12, d77, g54, g1, g40, g5
L2: b87, c65, d77, d34, d12, g54, g40, g5, g1
```

## Solution

```
#python
import string
def combinationSort(strList):
  # Create a dictionary with 26 keys from characters 'a' to 'z', each key has an empty list as value.
  groups = {k: [] for k in string.ascii_lowercase}

  # Using this dictionary to group strings with same initial character.  
  for i in range(len(strList)):
    char=strList[i][0]
    groups[char].append(strList[i])
  
  strList=[]
  # Recreate the list from all the strings in groups, iterating on groups from a to z.
  for char in groups.keys():
    for s in groups[char]:
      strList.append(s)
  
  L1 = strList.copy() # Saving intermediate result to return later.
  i = 1
  left = 0
  # As there can be no more than 100 strings with same initial character.
  # Using insertion sort within group.
  while i<len(strList):
    right = i
    while(right>left and strList[right][0] == strList[right-1][0] and int(strList[right-1][1:])<int(strList[right][1:])):
      strList[right], strList[right-1] = strList[right-1], strList[right]
      right -= 1
    i += 1
  
  return L1, strList
```

---

# GrPA 2

## Question

Complete the python function **findLargest(L)** below, which accepts a list L of unique numbers, that are sorted (ascending) and rotated n times, where n is unknown, and returns the largest number in list `L`. Rotating list `[2, 4, 5, 7, 8]` on e time gives us list `[8, 2, 4, 5, 7]`, and rotating the second time gives list `[7, 8, 2, 4, 5]` and so on. Try to give an *O(log n)* solution.

Hint: One of the *O(log n)* solutions can be implemented using binary search and using 'first or last' element to know, the directin of searching futher.

```
# input<L>: List L sorted and rotated.
# out: Return the largest number in list L.
def findLargest(L):
    # Your code goes here
```

***Sample input:***

```
7, 8, 2, 4, 5
```

***Sample output***

```
8
```

**Note:-** Do not use list slicing in Binary search implementation because the list slicing operation is of order O(n)

## Solution

```
#python
def findLargest(L):
  left = 0
  s = len(L)
  right = s-1
  
  # If list has only one element, that is the max.
  if (s==1):
    return L[0]
    
  while (left<=right):
    mid=(left+right)//2
    
    # if mid is at last index, next element to compare will be at index 0
    if (mid == s-1):
      nextToMid = 0
    else:
      nextToMid = mid+1

    if (L[mid] > L[nextToMid]):
      return L[mid]
    elif (L[mid] < L[0]):
      # our element is in left of mid
      right = mid-1
    else:
      # our element is in right of mid
      left = mid+1
```

---

# GrPA 3

## Question

Merging two sorted arrays in place.

Given a custom implementation of list named `MyList` objects you can perform read operations similar to the in-build lists in Python, example use `A[i]` to read element at index `i` in `MyList` object `A`. The only possible operation that you can use to edit data in `MyList` objects is by calling the `swap` method. For instance, `A.swap(indexA, B, indexB)` will swap values at `A[indexA]` and `B[indexB]` and `A.swap(index1, A, index2)` will swap values at `A[index1]` and `A[index2]`, where `indexA`, `indexB`, `index1`, `index2` are all integers.

Complete the Python function `mergeInPlace(A, B)` that accepts two `MyLists` `A` and `B` containing integers that are sorted in ascending order and merges them in place(without using any other list) such that after merging, `A` and `B` are still sorted in ascending order with the smallest element of both `MyLists` as the first element of `A`.

```
# Complete this function
def mergeInPlace(A, B):
    # Your code goes here
```

**Note:- Your function should not return any list and should only merge the given sorted lists inplace.**

***Sample Input:***

```
2 4 6 9 13 15
1 3 5 10
```

***Sample Output:***

```
[1, 2, 3, 4, 5, 6]
[9, 10, 13, 15]
```

***Sample Input:***

```
4 6
1 3 6 10
```

***Sample Output:***

```
1 3
4 6 6 10
```

## Solution

```
#python
def mergeInPlace(A, B):
  m = len(A)
  n = len(B)
  if (m < 1 or n < 1):
    return 
  
  # Find the smaller list of A and B.
  for i in range(0, m):
    # A and B are already sorted. B[0] will always be least in B, 
    # as we will maintain its sortedness .
    if (A[i] > B[0]):
      A.swap(i, B, 0)
       
      # move `B[0]` to its correct position in B to maintain the sortedness of B
      j = 0
      while(j < n - 1 and B[j] > B[j + 1]):
        B.swap(j+1, B, j)        
        j += 1
```