# Crying over sorted but stronger

***
### Better Comments
_This is the how I decided to use the extension._
- #Info related to the program (grey)
- #* Titles (green light)
- #? Advices or clarifications (blue)
- #todo Need to reforce (orange)
- #! Confused bout' something (red)
- #// Discarted (--)
- #- Success (yellow)
***
## 1. Basic operations
In this opportunity, I had to make some adjustments to the code, but I kept the same logic and structure.

```python

#* Basic operations
# I need to create a function that allows people to do basic operations (+, -, *, /) using two numbers.

def basic_operations(num1, num2, operation):
    try:
        if operation == "+":
            print(f"\nThe result is: {num1 + num2}")
        elif operation == "-":
            print(f"\nThe result is: {num1 - num2}")
        elif operation == "*":
            print(f"\nThe result is: {num1 * num2}")
        elif operation == "/":
            if num2 != 0:
                try:
                    print(f"\nThe result is:  {num1 // num2}")
                except ZeroDivisionError:
                    num2 = float(input("\nYou can not divide by zero. Enter the second number: "))
            else:
                raise ValueError("The second number cannot be zero.")
        else:
            raise ValueError("Enter a valid operation symbol (+, -, *, /).")
    except ValueError as e:
        print(e)

num1 = float(input("Enter the first number: "))
num2 = float(input("\nEnter the second number: "))
operation = input("\nEnter the operation symbol (+, -, *, /): ")
result = basic_operations(num1, num2, operation) #todo I need to study more about functions and return values.
```
___
## 2. Palindrome or not?
I decided to experiment with using a try-except block with lowercase letters, but ultimately found it unnecessary.

```python

#* Palindrome or not?
#A palindrome is a sequence of characters which reads the same forward and backward.


#* Palindrome or not?
#A palindrome is a sequence of characters which reads the same forward and backward.

def palindrome(word):
    try:
        word = word.lower() # Convert the word to lowercase to avoid errors when comparing the letters.
        lst = []
        for letter in word:
            lst.append(letter) # Convert the word to a list to compare the letters.
        for i in range(len(lst)//2): # If it is a palindrome, its first half will be the same as the second half.
            if lst[i] != lst[-i-1]:
                return False
        return True
    except:
        return False

word = input("Enter a word: ")
if palindrome(word):
    print(f"\n{word} is a palindrome.")
else:
    print(f"\n{word} is not a palindrome.")
```
___
## 3. Prime numbers
The code alredy had the most important exception.

```python

#* Prime number
#A prime number is a natural number greater than 1 that is not a product of two smaller natural numbers

def is_prime(num): #! I found this way to check if a number is prime in a website. It is more efficient than the one I was using.
    if num <= 1:
        return False
    for i in range(2, int(num**0.5) + 1): #? I need to check if the number is divisible by any number from 2 to the square root of the number.
        if num % i == 0:
            return False
    return True

def get_numbers():
    numbers = []
    while True:
        number = input("Enter an integer (or press 'q' to quit): ") #? I didn't want the user to write a specific number for the list to accept.
        if number.lower() == 'q':
            break
        try:
            number = int(number)
            numbers.append(number)
        except ValueError:
            print("Invalid input. Please enter an integer or 'q' to quit.")
    return numbers

def get_prime():
    numbers = get_numbers()

    prime_numbers = []
    for number in numbers:
        if is_prime(number):
            prime_numbers.append(number)

    prime_numbers.sort() #? I used the sort function to organize the numbers in ascending order.
    prime_numbers = set(prime_numbers) #? I used the set function to avoid repeated numbers.

    return prime_numbers

prime_numbers = get_prime()
print("Prime numbers:", prime_numbers)
```
___
## 4. Greater sum

I used Try - except back then when I wrote the code so it was kinda usefull. I just had to add the other ValueError.

```python

#* Greater sum of two numbers
#I need to create a function that receives a list of numbers and returns greater sum of two consecutive numbers.

def get_numbers(): #? I reused the get_numbers function from Prime_Numbers.py.
    numbers = []
    while True:
        number = input("Enter an integer (or press 'q' to quit): ")
        if number.lower() == 'q':
            break
        try:
            number = int(number)
            numbers.append(number)
        except ValueError:
            print("Invalid input. Please enter an integer or 'q' to quit.")
    numbers = list(set(numbers)) #? I used the set function to avoid repeated numbers.
    return numbers

try:
    def greater_sum(numbers):
        if len(numbers) < 2:
            return None  # Not enough numbers to calculate sum
        max_sum = numbers[0] + numbers[1]
        for i in range(1, len(numbers)-1):
            current_sum = numbers[i] + numbers[i+1]
            max_sum = max(max_sum, current_sum)
        return max_sum
except ValueError:
    print("You need to write at least two numbers.")

numbers = get_numbers()
result = greater_sum(sorted(numbers))
print("The numbers are:", numbers)
print("The greater sum of two consecutive numbers is:", result)
```
___
## 5. Anagrams
Adding the exception was not as hard as it could be thanks to the code that I had wrote.

```python

#* Anagrams
# I need to create a function that returns the anagrams found in a list of words and also I need to use exceptions to handle possible errors.

def get_words():
    while True:
        try:
            words = input("Write words separated by commas: ").split(',') #? Split the input by commas
            words = [word.strip() for word in words]
            if any(word.isdigit() for word in words): #? Check if there are numbers in the list
                raise ValueError("Please enter words only. Numbers are not allowed.") #? I used the ValueError exception to handle the error.
            else:
                break
        except ValueError as e:
            print(e)
    return words

def is_anagram(words):
    anagrams = set()
    for i in range(len(words)):
        for j in range(i+1, len(words)):
            if sorted(words[i]) == sorted(words[j]):
                anagrams.add(words[i])
                anagrams.add(words[j])
    return list(anagrams)

words = get_words()
print(f"\nThe original list is: {words}")
anagrams = is_anagram(words)
print(f"\nThe anagrams are: {anagrams}")
```
***

# Stronger Shape

***

## shape.py

I added a Try-Except for the get point() method to avoid the ValueError exception.

```python
import math
from typing import List

#*Figures and shapes
#Practizing polimorphism and heritance

class Point:
    def __init__(self, x, y):
        self._x = x
        self._y = y

    def get_x(self):
        return self._x

    def get_y(self):
        return self._y

    @staticmethod
    def get_point():
        while True:
            try:
                x = float(input("Enter the x-coordinate of the vertex: "))
                y = float(input("Enter the y-coordinate of the vertex: "))
                return Point(x, y)
            except ValueError:
                print("Invalid input. Please enter a valid number.")

class Line:
    def __init__(self, start: Point, end: Point):
        self._start = start
        self._end = end

    def get_start(self):
        return self._start

    def get_end(self):
        return self._end

    def compute_length(self):
        length = math.sqrt((self._end.get_x() - self._start.get_x())**2 + (self._end.get_y() - self._start.get_y())**2)
        return abs(length)

class Shape(Line):
    def __init__(self, is_regular: bool, vertices: List[Point], edges: List[Line], inner_angles: List[float], width: float, height: float):
        self._is_regular = is_regular
        self._vertices = vertices
        self._edges = edges
        self._inner_angles = inner_angles
        self._width = width
        self._height = height

    def get_is_regular(self):
        return self._is_regular

    def set_is_regular(self, is_regular):
        self._is_regular = is_regular

    def get_vertices(self):
        return self._vertices

    def set_vertices(self, vertices):
        self._vertices = vertices

    def get_edges(self):
        return self._edges

    def set_edges(self, edges):
        self._edges = edges

    def get_inner_angles(self):
        return self._inner_angles

    def set_inner_angles(self, inner_angles):
        self._inner_angles = inner_angles

    def get_width(self):
        return self._width

    def set_width(self, width):
        self._width = width

    def get_height(self):
        return self._height

    def set_height(self, height):
        self._height = height

    def compute_area(self):
        pass

    def compute_perimeter(self):
        pass

    def compute_inner_angles(self):
        pass
```
___
## triangle.py

I wrapped the code block in a try-except to handle exceptions of type ValueError when the user enters an invalid option when asking if the rectangle is regular. If the user enters something other than 'y' or 'n', an exception is raised with a custom error message.

```python
# triangle.py

from shapes.shape import Shape, Point, Line, math, List

class Triangle(Shape):
    def __init__(self, is_regular: bool, vertices: List[Point], edges: List[Line], inner_angles: List[float]):
        super().__init__(is_regular, vertices, edges, inner_angles, 0, 0)

        try:
            self._is_regular = input("Is the triangle regular? (y/n): ") #? If the triangle is regular, then the triangle is equilateral.
            if self._is_regular not in ["y", "n"]:
                raise ValueError("Invalid input. Please enter 'y' or 'n'.")

            if self._is_regular == "y":
                self._is_regular = True

                print("\nThis is an equilateral triangle.")

                length = float(input("\nEnter the length of the first edge: "))

                print("\nEnter the coordinates of the first vertex")
                first_vertex = Point.get_point()
                second_vertex = Point(first_vertex.get_x() + length, first_vertex.get_y())
                third_vertex = Point(first_vertex.get_x() + length/2, first_vertex.get_y() + length)

                self._vertices = [first_vertex, second_vertex, third_vertex]
                self._edges = [length, length, length]
                self._inner_angles = [60, 60, 60]

            elif self._is_regular == "n":
                self._is_regular = False
                first_length = float(input("Enter the length of the first edge: "))

                print("\nEnter the coordinates of the first vertex")
                first_vertex = Point.get_point()
                second_vertex = Point(first_vertex.get_x() + first_length, first_vertex.get_y())
                print("\nEnter the coordinates of the third vertex")
                third_vertex = Point.get_point()
                vertices = [first_vertex, second_vertex, third_vertex]

                compute_length = Line.compute_length
                half = (first_vertex.get_x() + first_length) - (first_length / 2) #? This is the half of the base of the triangle.
                if third_vertex.get_x() == half:
                    print ("\nThis is an isosceles triangle.")

                    second_length = compute_length(Line(first_vertex, third_vertex))
                    third_length = second_length

                    self._vertices = [first_vertex, second_vertex, third_vertex]
                    self._edges = [first_length, second_length, third_length]

                    self._inner_angles = [0, 0, 0]
                    self._inner_angles[0] = math.degrees(math.acos((first_length**2 - second_length**2 - third_length**2) / (-2 * second_length * third_length)))
                    self._inner_angles[1] = self._inner_angles[0]
                    self._inner_angles[2] = 180 - self._inner_angles[0] * 2

                elif third_vertex.get_x() != half and third_vertex.get_x() != first_vertex.get_x():
                    print("\nThis is a scalene triangle.")
                    second_length = compute_length(Line(first_vertex, third_vertex))
                    third_length = compute_length(Line(second_vertex, third_vertex))
                    self._vertices = [first_vertex, second_vertex, third_vertex]
                    self._edges = [first_length, second_length, third_length]

                    self._inner_angles = [0, 0, 0]
                    self._inner_angles[0] = math.degrees(math.acos((first_length**2 - second_length**2 - third_length**2) / (-2 * second_length * third_length)))
                    self._inner_angles[1] = math.degrees(math.acos((second_length**2 - first_length**2 - third_length**2) / (-2 * first_length * third_length)))
                    self._inner_angles[2] = math.degrees(math.acos((third_length**2 - first_length**2 - second_length**2) / (-2 * first_length * second_length)))
                else:
                    third_vertex.get_x() != half and third_vertex.get_x() == first_vertex.get_x()
                    print("\nThis is a right triangle.")
                    second_length = compute_length(Line(first_vertex, third_vertex))
                    third_length = math.sqrt(first_length**2 + second_length**2)
                    self._vertices = [first_vertex, second_vertex, third_vertex]
                    self._edges = [first_length, second_length, third_length]

                    self._inner_angles = [0, 0, 0]
                    self._inner_angles[0] = 90
                    self._inner_angles[1] = math.degrees(math.atan(first_length / third_length))
                    self._inner_angles[2] = math.degrees(math.atan(second_length / third_length))

        except ValueError as e:
            print(f"Error: {e}")

    def compute_perimeter(self):
        return sum(self._edges)

    def compute_area(self): #? This is the Heron's formula.
        s = self.compute_perimeter() / 2
        return math.sqrt(s * (s - self._edges[0]) * (s - self._edges[1]) * (s - self._edges[2]))

    def __str__(self):
        vertices_str = ", ".join([f"({v.get_x()}, {v.get_y()})" for v in self._vertices])
        edges_str = ", ".join([f"{ed}" for ed in self._edges])
        angles_str = ", ".join([f"{angles}" for angles in self._inner_angles])
        permiter = self.compute_perimeter()
        area = self.compute_area()
        return f"\nTriangle: \nVertices: {vertices_str}\n\nEdges: {edges_str}\n\nInner Angles: {angles_str}\n\nPerimeter: {permiter}\n\nArea: {area}"

triangle = Triangle(True, [], [], [])
print(triangle)
```
I added the triangle class to its module and tried to import Shape, Point, Line, math and List from shapes.

___
## rectangle.py

I wrapped the code block in a try-except to handle exceptions of type ValueError when the user enters an invalid option when asking if the rectangle is regular. If the user enters something other than 'y' or 'n', an exception is raised with a custom error message.

```python
from shapes.shape import Shape, Point, Line, List

class Rectangle(Shape):
    def __init__(self, is_regular: bool, vertices: List[Point], edges: List[Line], inner_angles: List[float], width: float, height: float):
        super().__init__(is_regular, vertices, edges, inner_angles, width, height)
        self._width = width
        self._height = height
        self._vertices = vertices
        self._edges = edges
        self._inner_angles = inner_angles

        try:
            self._is_regular = input("\nIs the rectangle regular? (y/n): ") #? If the rectangle is regular, then the rectangle is a square.
            if self._is_regular not in ["y", "n"]:
                raise ValueError("Invalid input. Please enter 'y' or 'n'.")

            if self._is_regular == "y":
                self._is_regular = True

                print("\nThis is a square.")
                length = float(input("Enter the length of one side: "))
                print("Enter the coordinates of the first vertex")
                first_vertex = Point.get_point()

                second_vertex = Point(first_vertex.get_x() + length, first_vertex.get_y())
                third_vertex = Point(first_vertex.get_x(), first_vertex.get_y() + length)
                fourth_vertex = Point(first_vertex.get_x() + length, first_vertex.get_y() + length)

                self._vertices = [first_vertex, second_vertex, third_vertex, fourth_vertex]
                self._edges = [length, length, length, length]
                self._inner_angles = [90, 90, 90, 90]
                self._width = length
                self._height = length

            elif self._is_regular == "n":
                self._is_regular = False

                width = float(input("\nEnter the width of the rectangle: "))
                height = float(input("Enter the height of the rectangle: "))

                print("\nEnter the coordinates of the first vertex: ")
                first_vertex = Point.get_point()
                second_vertex = Point(first_vertex.get_x() + width, first_vertex.get_y())
                third_vertex = Point(first_vertex.get_x(), first_vertex.get_y() + height)
                fourth_vertex = Point(first_vertex.get_x() + width, first_vertex.get_y() + height)

                self._vertices = [first_vertex, second_vertex, third_vertex, fourth_vertex]
                self._edges = [width, width, height, height]
                self._inner_angles = [90, 90, 90, 90]
                self._width = width
                self._height = height

        except ValueError as e:
            print(f"Error: {e}")

    def compute_perimeter(self):
        return sum(self._edges)

    def compute_area(self):
        return self._width * self._height

    def __str__(self):
        vertices_str = ", ".join([f"({v.get_x()}, {v.get_y()})" for v in self._vertices])
        edges_str = ", ".join([f"{ed}" for ed in self._edges])
        angles_str = ", ".join([f"{angles}" for angles in self._inner_angles])
        perimeter = self.compute_perimeter()
        area = self.compute_area()
        return f"Rectangle: \nVertices: {vertices_str}\n\nEdges: {edges_str}\n\nInner Angles: {angles_str}\n\nPerimeter: {perimeter}\n\nArea: {area}"

rectangle = Rectangle(True, [], [], [], 0, 0)
print(rectangle)
```
___
## main.py

<img width="844" alt="main c" src="https://github.com/LauSofiJM/Package-Shape/assets/159340280/b40afeea-0b4f-4d96-a20c-5c4425fc8bd0">

```python
# main.py

from shapes import triangle, rectangle
triangle = triangle(is_regular=False, vertices=[], edges=[], inner_angles=[])
print(triangle)
rectangle = rectangle(is_regular=False, vertices=[], edges=[], inner_angles=[], width=0, height=0)
print(rectangle)
```
### That was it. Thanks for reading.
