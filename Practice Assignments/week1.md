## Week 1 Practice Assignment

1) 
```
def check(n):
    while n != 0:
        d = n % 10
        if d % 2 != 1:
            return False
        n = n // 10
    return True
```
If `n` is a positive integer then which of the following statement is correct about function check ?
1. Function check returns True if the number of digits in n is odd.
2. Function check returns True if all digits of n are even.
3. Function check returns True if all digits of n are odd.
4. Function check returns True if the number of digits in n is even.

**Ans:- 3. Function check returns True if all digits of n are odd.**

---

2) 
```
x = range(5)
s = 0
for i in x:
    s += i
```
What will be the value of i after execution of the given code-snippet?
1. 2
2. 5
3. 4
4. Code has error

**Ans:- 3. 4**

---

3) Match the following

| Method | Description |
|-----|-----|
| (A) `__init__()` | (i) Implements addition with the `+` operator |
| (B) `__add__()` | (ii) Initialize the object |
| (C) `__sub__()` | (iii) Implements multiplication with the `*` operator |
| (D) `__mul__()` | (iv) Implements subtraction with the `-` operator |
1. A-(i) B-(ii) C-(iii) D-(iv)
2. A-(ii) B-(i) C-(iv) D-(iii)
3. A-(iii) B-(i) C-(ii) D-(iv)
4. A-(ii) B-(iii) C-(iv) D-(i)

**Ans:- 2. A-(ii) B-(i) C-(iv) D-(iii)**

---

4) 
```
L = [[10.5], '10.5', 10.5, (10.5)]
i = 0

while i < 4:
    try:
        item = int(L[i])
        print('No Error')
    except TypeError:
        print('Error1')
    except ValueError:
        print('Error2')

    i += 1
```
What is the output of given code?

1. 
```
Error1
Error2
No Error
Error1
```
2. 
```
Error1
Error2
No Error
Error2
```
3. 
```
Error1
Error2
No Error
No Error
```
4. 
```
Error1
Error2
Error2
Error1
```

**Ans:- 3**
```
Error1
Error2
No Error
No Error
```

---

5) Which of the following options will validate whether n is a perfect square or not? Where n is a positive integer. [MSQ]

1. 
```
def h(n):
    return (n ** .5) == int (n ** .5)
```
2.
```
def h(n):
    return (n ** .5) == int (n) ** .5
```
3.
```
def h(n):
    for i in range(1, n + 1):
        if i  *  i == n:
            return True
    return False
```
4.
```
def h(n):
    for i in range(1, n + 1):
        if i * i > n:
            break
        elif i * i == n:
            return True
    return False
```
**Ans:- 1, 3, 4**

1.
```
def h(n):
    return (n ** .5) == int (n ** .5)
```
3.
```
def h(n):
    for i in range(1, n + 1):
        if i  *  i == n:
            return True
    return False
```
4.
```
def h(n):
    for i in range(1, n + 1):
        if i * i > n:
            break
        elif i * i == n:
            return True
    return False
```