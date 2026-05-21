# PPA 1
---
## Question
' Twin primes ' are pairs of prime numbers that differ by 2. For example (3, 5), (5, 7), and (11,13) are twin primes.

Write a function ' Twin_Primes(n, m) ' where n and m are positive integers and n < m , that returns all unique twin primes between m and n (both inclusive). The function returns a list of tuples and each tuple (a,b) represents one unique twin prime where n <= a < b <= m.

---

## Solution
'''
def prime(n):
  if n < 2:
    return False
  for i in range(2,n//2+1):
    if n%i==0:
      return False
  return True
    
def Twin_Primes(n, m):
  Res=[]
  for i in range(n,m-1):
    if prime(i)==True:
      if prime(i+2)==True:
        Res.append((i,i+2))
  return(Res)
n=int(input())
m=int(input())
print(sorted(Twin_Primes(n, m)))
'''

# PPA 2
---
## Question
Create a ' Triangle ' class that accepts three side-lengths of the triangle as ' a ', ' b ' and ' c ' as parameters at the time of object creation. Class ' Triangle ' should have the following methods:
- ' Is_valid() ' :- Returns ' valid ' if triangle is valid otherwise returns ' Invalid '.
    - A triangle is valid when the sum of its two side-length are greater than the third one. That means the triangle is valid if all three condition are satisfied:
        - a + b > c
        - a + c > b
        - b + c > a
- ' Side_Classification() ' :- If the triangle is invalid then return Invalid. Otherwise, it returns the type of triangle according to the sides of the triangle as follows:
    - Return ' Equilateral ' if all sides are of equal length.
    - Return ' Isoceles ' if any two sides are of equal length and third is different.
    - Return ' Scalene ' if all sides are of different lengths.
- ' Angle_Classification() ' :- If the triangle is invalid then return ' Invalid '. Otherwise, return type of triangle using Pythagoras theorem.

For example if ' a <=b <=c '. then
    - If a<sup>2</sup> + b<sup>2</sup> > c<sup>2</sup> return ' Acute '
    - a<sup>2</sup> + b<sup>2</sup> = c<sup>2</sup> return ' Right '
    - a<sup>2</sup> + b<sup>2</sup> < c<sup>2</sup> return ' Obtuse '

In the formula of angle classification, the square of the largest side length should be compared to the sum of squares of the other two side lengths.

- ' Area() ' :- If the triangle is invalid then return ' Invalid '. Otherwise, return the area of the triangle.
    - Area = sqrt( s ( s-a ) ( s-b ) ( s-c ))
    Where s = (a + b + c )/2

## Solution
---
"""
class Triangle:
	def __init__(self,a,b,c):
		self.a = a
		self.b = b
		self.c = c
	def Is_valid(self):
		if self.a >= self.b + self.c:
			return 'Invalid'
		if self.b >= self.a + self.c:
			return 'Invalid'
		if self.c >= self.b + self.a:
			return 'Invalid'
		return 'Valid'
	def Side_Classification(self):
		if self.Is_valid() == 'Valid':
			if self.a == self.b == self.c:
				return 'Equilateral'
			elif (self.a == self.b) or (self.b == self.c) or (self.a == self.c):
				return 'Isosceles'
			else:
				return 'Scalene'
		else:
			return 'Invalid'
	def Angle_Classification(self):
		if self.Is_valid() == 'Valid':
			l = [self.a**2, self.b**2, self.c**2]
			l.sort()
			if l[0] + l[1] > l[2]:
				return "Acute"
			elif l[0] + l[1] == l[2]:
				return "Right"
			elif l[0] + l[1] < l[2]:
				return "Obtuse"
		else:
			return 'Invalid'	
	def Area(self):
		if self.Is_valid() == 'Valid':
			s = (self.a + self.b + self.c)/2
			return (s*(s-self.a)*(s-self.b)*(s-self.c)) ** 0.5
		else:
			return 'Invalid'
a=int(input())
b=int(input())
c=int(input())
T=Triangle(a,b,c)
print(T.Is_valid())
print(T.Side_Classification())
print(T.Angle_Classification())
print(T.Area())
"""