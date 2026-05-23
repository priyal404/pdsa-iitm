1) 

```
def fun(S):
    p = 0
    S = S.lower()
    for i in range(len(S)):
        if S[i] not in S[:i]:
            p += 1
    return p
```

S is a non-empty string of English letters without any space. What fun(S) will return after execution of the above code?

1. Total number of letters in the string S .
1. Total number of distinct letters in the string S .
1. Total number of letters that are repeated in the string S more than one time.
1. Difference of total letters in the string S and distinct letters in the string S.

Feedback: During traversing of the input string , p is incremented by one only when any letter occurs first time. Hence, the return value of p represents the total number of distinct letters in the string S.

**Ans:- 2. Total number of distinct letters in the string S .**

---

2) Which of the following is/are valid reason(s) for NameError exception? [MSQ]

1. Variable is not defined.
1. Calling a function before declaration.
1. Misspelled built-in functions name
1. Variables are defined globally in the program .

Feedback: Options (a), (b) and (c) are valid reasons for NameError exception. But option (d) is not correct because the global variable can be accessed from any scope in the program, so it will not return any error.

**Ans:- 1, 2, 3.**

1. Variable is not defined.
1. Calling a function before declaration.
1. Misspelled built-in functions name

---

3)

```
def f(n):
    S = 0
    for i in range(2,n):
        if n % i == 0 and i % 2 == 1:
            S = S + 1
    return(S)
```

What is f(60) - f(59) , given the definition of f above? (Type: Numeric)

**Ans:- 3**

---

4)

```
x = 1
while True:
    if x % 5 == 0:
        break
    print(x, end = ' ')
    x += 1
```

What will be the output of the above code-snippet?

1. Syntax error
1. 2 1
1. 0 3 1
1. None of these

Feedback: In given code-snippet, in line 3, comparison operator = = has one extra space in between, because of that, the code will raise a Syntax error.

**Ans:- 1. Syntax error**

---

5) 

```
class Person:
    def __init__(self,name):
        self.name = name
    def say_hi(self):
        print('Hello, ', self.name)

p = Person('Good morning')
p.say_hi()
```

What will be the output of the above code-snippet?

1. Good morning
1. Hello, Good morning
1. Hello Good morning
1. Good

**Ans:- 2. Hello, Good morning**

---

6) 

```
a = [1, 2, 3]
try:
    print("Second element = %d" %(a[1])")
    print("Fourth element = %d" %(a[3])")
except:
    print("An error occurred")
```

What will be the output of the above code-snippet?

1. 

```
Second element = 2
```
2. 

```
An error occurred
```
3. 

```
Second element = 2
An error occurred
```
4. 

```
Second element = 2
Fourth element = 3
An error occurred
```

Feedback: List a has three elements (index 0 to 2). Inside try block first print statement will execute correctly after that second print statement will raise an index error because index 3 is not available in list a, Due to this error except block's print statement will execute. Hence, option (c) is correct.

**Ans:- 3.**

```
Second element = 2
An error occurred
```

---

7)

```
def special3Bad(L):
    try:
        if L[0] % L[1] == 0 and L[1] != 0:
            if L[0] / (L[1] ** 2 - L[2]) == 0:
                return True
        return False
    except ZeroDivisionError:
        print('ZeroDivisionError')
    except:
        print('Some other exception occurred')
    else:
        print('No exception occurred')

special3Bad(L)
```

Given above is a function that checks whether a list satisfies some property. There is an error in this function. Select the list(s) L = [n1, n2, n3] , where n1 , n2 and n3 are all integers, for which special3Bad(L) produces a ZeroDivisionError exception. [MSQ]

1. `L = [4, 2, 8]`
1. `L = [4, 2, 4]`
1. `L = [8, 4, 16]`
1. `L = [48, 6, 36]`
1. `L = [44, 6, 36]`

Feedback: The ZeroDivisionError is due to if a number being divided by zero. In code line number 4, if divisor (L[1] ** 2 - L[2]) becomes zero, then it produces a ZeroDivisionError exception. For options (b), (c) and (d), divisor (L[1] ** 2 - L[2]) become zero. Hence, For options (b), (c) and (d) are correct.

**Ans:- 2, 3, 4.**

2. `L = [4, 2, 4]`
1. `L = [8, 4, 16]`
1. `L = [48, 6, 36]`

---

8)

```
def isSymmetricBad(L):
    try:
        while len(L) > 0:
            if L.pop(0) != L.pop(-1):
                return False
        return True
    except IndexError:
        print('IndexError')
    except:
        print('Some other exception occurred')
    else:
        print('No exception occurred')

isSymmetricBad(L)
```

Given above is a function to check whether a list is a palindrome. There is an error in this function. Select the list(s) L = [n1, n2,..., n2, n1] , for which isSymmetricBad(L) produces an IndexError exception. [MSQ]

1. `L = [1, 2, 3, 4, 3, 2, 1]`
1. `L = [2, 2, 2, 2, 2, 2]`
1. `L = [1, 1, 1, 1, 1, 1, 1]`
1. `L = [8]`
1. `L = [2, 4, 6]`

Feedback: An IndexError occurs if the code is trying to access an index that does not exist. The pop(i) function removes the ith indexed element from the list and returns the removed element. Line number 4 compares the first and last indexed elements of the list after removing them from the list.

If input list length is odd and the first removed and last removed element are equal, then for every cycle of while loop, the first and the last element will be removed. In the last cycle of the while loop, only one element will remain in the list, So pop(0) will remove this single element from the list then pop(-1) will produce an index error because the list is already empty. Hence, options (a), (c) and (d) are correct.

**Ans:- 1, 3, 4.**

1. `L = [1, 2, 3, 4, 3, 2, 1]`
3) `L = [1, 1, 1, 1, 1, 1, 1]`
4. `L = [8]`

---

9)

```
def gcd(m,n):
    (a,b) = (max(m,n), min(m,n))
    if a % b == 0:
        return(b)
    else:
        return(gcd(b,a % b))

print(gcd(24,130))
```

How many times gcd() function will be called? (Type: Numeric)

**Ans:- 3**

---

10)

```
class Enrollment:
    count = 0

    def __init__(self,n,c):
        self.name = n
        self.course = c
        Enrollment.count += 1

    def display(self):
        print(self.name)
        print(self.course)
```

Which of the following option(s) is/are correct about the given code? [MSQ]

1. count , name and course are object variables.
1. name and course are class variable and count is an object variable.
1. name and course are object variables, and count is a class variable.
1. count , name and course are class variables.
1. count represents the number of objects created for class Enrollment

**Ans:- 3, 5.**

3) name and course are object variables, and count is a class variable.
5. count represents the number of objects created for class Enrollment

---

11) 

```
def fun(n): # n is an integer
    if n == 0:
        return 0
    return (n % 10) + fun(n // 100)
```

What does the above code compute?

1. The sum of all digits
1. The sum of alternate digits starting from the last digit
1. The sum of digits at even indexed positions (from left, 0-based)
1. The sum of alternate digits starting from the first digit from left

Feedback: This function picks every second digit from the end (right to left) because it skips 2 digits each time ( n // 100 ).

**Ans:- 2. The sum of alternate digits starting from the last digit**

---

12)

```
def fun(n):
    if n == 0:
        return 0
    if (n % 10) % 2 == 0:
        return 1 + fun(n // 10)
    else:
        return fun(n // 10)
```

What is the final value returned by the function?

1. Number of even digits
1. Sum of even digits
1. Sum of odd digits
1. Number of odd digits

Feedback: The function iterates through the digits of the number n from right to left. The condition (n % 10) % 2 == 0 checks if the last digit is even. If it is, the function returns 1 (counting the even digit) plus the result of calling itself with the remaining digits ( n // 10 ). If the last digit is odd, it simply calls itself with the remaining digits without adding anything. Therefore, the function counts the total number of even digits in the input number.

**Ans:- 1. Number of even digits**

---

13) Consider the code given below

```
def fun(n):
    if n <= 1:
        return 0
    return fun(n - 1) + fun(n - 2)
```

How many recursive calls are made (excluding the initial call to fun(5) ) ? (Type: Numeric)

Feedback: 

Call Tree for fun(5) :

```text
fun(5)
├── fun(4)
│   ├── fun(3)
│   │   ├── fun(2)
│   │   │   ├── fun(1) → 0
│   │   │   └── fun(0) → 0
│   │   └── fun(1) → 0
│   ├── fun(2)
│   │   ├── fun(1) → 0
│   │   └── fun(0) → 0
└── fun(3)
    ├── fun(2)
    │   ├── fun(1) → 0
    │   └── fun(0) → 0
    └── fun(1) → 0
```

Total number of calls excluding the root fun(5) = 14

**Ans:- 14**

---

14) Consider the code given below.

```
def fun(n):
    if n <= 1:
        return 0
    if n % 2 == 0:
        return fun(n // 2)
    else:
        return 1 + fun(n // 2) + fun(n // 2)

fun(18)
```

How many recursive calls (excluding the initial fun(18) ) are made? (Type: Numeric)

**Ans:- 7**

---

15) Consider the code given below.

```
class Box:
    def __init__(self, size):
        self.size = size
    
    def double(self):
        self.size = self.size * 2
    
x = Box(5)
y = x
y.double()
x.double()

print(x.size, y.size)
```

Select all correct statements. [MSQ]

1. Output will be 20 20
1. Output will be 10 10
1. x and y refer to the same object
1. x and y are independent copies of objects
1. Method double() modifies the object in-place

Feedback: 
y = x → x and y reference the same object
y.double() → doubles size to 10
x.double() → doubles size to 20
So both x.size and y.size print 20
Method double() modifies the object in-place

**Ans:- 1, 3, 5.**

1. Output will be 20 20
3) x and y refer to the same object
5. Method double() modifies the object in-place