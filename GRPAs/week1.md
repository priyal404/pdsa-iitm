# GrPA 1

---

## Question

---

Write a function find_Min_Difference(L, P) that accepts a list L of integers and P (positive integer) where the size of L is greater than P. The task is to pick P different elements from the list L, where the difference between the maximum value and the minimum value in selected elements is minimum compared to other differences in possible subset of p elements. The function returns this minimum difference value.

Note - The list can contain more than one subset of p elements that have the same minimum difference value.

** Example **

Let L = [3, 4, 1, 9, 56, 7, 9, 12, 13] and P = 5

If we see the following two subsets of 5 elements from L

[3, 4, 7, 9, 9] or [7, 9, 9, 12, 13]

Here, the difference between the maximum value and the minimum value in both subset is 9 - 3 = 6 or 13 - 7 = 6 which is minimum. So the output will be 6.

** Sample Input **
```[3, 4, 1, 9, 56, 7, 9, 12]
5```
** Output **
```6```

## Solution

---

```
def find_Min_Difference(L,P):
    L.sort()
    N = P
    M = len(L)
    min_diff = max(L) - min(L)
    for i in range(M-N+1):
        if L[i+N-1] - L[i] < min_diff:
            min_diff = L[i+N-1] - L[i]
    return min_diff
L=eval(input().strip())
P=int(input())
print(find_Min_Difference(L,P))
```

# GrPA 2

---

## Question

---

**Goldbach's conjecture** is one of the oldest and best-known unsolved problems in number theory. It states that every even number greater than 2 is the sum of two prime numbers.

**For Example:**

12 = 5 + 7

26 = 3 + 23 or 7 + 19 or 13 +13

Write a function **`Goldbach(n)`** where n is a positive even number(n > 2) that returns a list of tuples. In each tuple (a,b) where a <= b, a and b should be prime numbers and the sum of a and b should be equal to n.

** Sample Input 1 **
``` 12 ```
** Output **
``` [(5,7)] ```
** Sample Input 2 **
``` 26 ```
** Output **
``` [(3,23), (7,19), (13,13)] ```

## Solution

---

```
def prime(n):
    if n < 2:
        return False
    for i in range(2,n//2+1):
        if n%i==0:
            return False
    return True

def Goldbach(n):
    Res=[]
    for i in range((n//2)+1):
            if prime(i)==True:
                if prime(n-i)==True:
                    Res.append((i,n-i))
    return(Res)
n=int(input())
print(sorted(Goldbach(n)))
```

# GrPA 3

---

## Question

---

Write a function named `odd_one(L)` that accepts a list `L` as argument. Except for one element, all other elements in `L` are of the same data type. The function `odd_one` should return the data type of this odd element.

For example, if `L` is equal to [1, 2, 3.4, 5, 10], then the function should return the string float. This is because the element 3.4 is the odd one here, all other elements are integers.

**Note**
`L` has at least three elements.
For each test case, the elements in the list will only be of one of these four types: int, float, str, bool.
The function must return one of these four strings: int, float, str, bool.
Hint: `type(1)` == `int` evaluates to True.

## Solution

---

```
def odd_one(L):
  P = {}
  for elem in L:
    if type(elem) not in P:
      P[type(elem)] = 0
    P[type(elem)] += 1
  for key, value in P.items():
    if value == 1:
      return key.__name__
print(odd_one(eval(input().strip())))
```