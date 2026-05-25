# PPA 1

## Question

Binary search

Write a Python function binarySearchIndexAndComparison(L, K) that accepts a list `L` sorted in ascending order and an integer `k` and returns a tuple (True/False, numComparisons). The first part of this tuple will be `True` if integer k is present in list `L`, `False` otherwise. The second part of this tuple is an integer which gives the number of elements in `L` that are actually compared to `k` while searching `k` in the list `L` using **binary search**.

For consistency use (left+right)//2 to calculate the middle index.

**Example:**

For given `L` and `k`, your function should return as mentioned in the table below.

`L = [2, 6, 8, 11, 17, 23, 33, 44, 46, 50, 65]`

| k | Return |
| --- | --- |
| 11 | (True, 3) |
| 23 | (True , 1) |
| 100 | (False, 4) |

## Solution

```
#python
def binarySearchIndexAndComparisons(L,k):
  s = len(L)
  if(s < 1):
    return (False, 0)

  left = 0
  right = s - 1
  c = 0
  while(left <= right):
    mid = (left + right)//2
    c += 1
    if (k == L[mid]):
      return (True,c)
    elif (k < L[mid]):
      right = mid - 1
    else:
      left = mid + 1
  return(False, c)
```
---

# PPA 2

## Question

Consider a list `L` containing `n` integers, where each integer `i` is in the range `[0, r)` that is `0 <= i < r`, `r<1000` and `n>>r` (n is much greater than r). Write a Python function `sortInRange(L, r) to sort the list 'L' in ascending order. Try to write a solution that runs in *O(n + r)* asymptotic complexity.
***Sample Input:***

```
L: 2, 0, 1, 1, 2, 3, 0, 2, 1, 0, 2, 3, 1, 2
r: 4
```

***Sample Output:***
```
0, 0, 0, 1, 1, 1, 1, 2, 2, 2, 2, 2, 3, 3
```

**Note:-** In function, no need to return any list, just sort input list 'L' in place.

## Solution

```
#python
def sortInRange(L, r):
  # Create a dictionary with r keys for each integer in range r, initialize every value to 0
  countDict = [0 for i in range(r)]

  # Iterate over the array and count each integer in the list
  for num in L:
    countDict[num] += 1
  
  index=0
  for key in range(r):
    for i in range(countDict[key]):
      L[index] = key
      index += 1
```