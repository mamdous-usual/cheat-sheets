# Python Cheat Sheet

## 1. Basic Syntax

```python
print("Hello, World!")

# Single-line comment

"""
Multi-line comment
"""
```

## 2. Variables & Data Types

```python
name = "Alex"
age = 22
price = 99.99
is_active = True
value = None
```

| Type | Description |
|---|---|
| `int` | Integer numbers |
| `float` | Decimal numbers |
| `str` | Text |
| `bool` | True or False |
| `list` | Ordered, mutable collection |
| `tuple` | Ordered, immutable collection |
| `set` | Unique elements |
| `dict` | Key-value pairs |
| `NoneType` | Represents no value |

```python
type(age)          # Check data type
int("10")          # Convert to integer
str(100)           # Convert to string
float("10.5")      # Convert to float
```

## 3. Operators

| Operator | Description |
|---|---|
| `+` `-` `*` `/` `%` `//` `**` | Arithmetic |
| `==` `!=` `>` `<` `>=` `<=` | Comparison |
| `and` `or` `not` | Logical |
| `=` `+=` `-=` `*=` `/=` | Assignment |
| `in` `not in` | Membership |
| `is` `is not` | Identity |

## 4. User Input & Output

```python
name = input("Enter name: ")
age = int(input("Enter age: "))

print("Hello", name)
print(f"My age is {age}")
```

- `input()` — Takes user input as a string.
- `print()` — Displays output.
- `f""` — Formats strings using variables.

## 5. Strings

```python
text = "Hello Python"

text.upper()
text.lower()
text.strip()
text.replace("Hello", "Hi")
text.split()
text.startswith("Hello")
text.endswith("Python")
text.find("Python")
text.count("o")
text[0]
text[0:5]
len(text)
```

### String Formatting

```python
name = "Alex"
age = 22

message = f"{name} is {age} years old"
```

## 6. Lists

Ordered and mutable collections.

```python
numbers = [1, 2, 3, 4, 5]

numbers.append(6)
numbers.insert(0, 10)
numbers.remove(3)
numbers.pop()
numbers.sort()
numbers.reverse()

numbers[0]       # Access element
numbers[1:3]     # Slicing
len(numbers)     # Length
```

### List Comprehension

```python
squares = [x**2 for x in range(5)]

evens = [x for x in numbers if x % 2 == 0]
```

## 7. Tuples

Ordered and immutable collections.

```python
numbers = (1, 2, 3, 4)

numbers[0]
numbers.count(2)
numbers.index(3)

# Unpacking
a, b, c = (10, 20, 30)
```

## 8. Sets

Unordered collections containing unique elements.

```python
numbers = {1, 2, 3, 4}

numbers.add(5)
numbers.remove(2)
numbers.discard(10)
numbers.pop()

# Set operations
a | b       # Union
a & b       # Intersection
a - b       # Difference
a ^ b       # Symmetric difference
```

## 9. Dictionaries

Store data in key-value pairs.

```python
student = {
    "name": "Alex",
    "age": 22,
    "course": "Python"
}

student["name"]
student.get("age")

student["city"] = "Delhi"
student.update({"age": 23})
student.pop("course")

student.keys()
student.values()
student.items()
```

### Dictionary Iteration

```python
for key, value in student.items():
    print(key, value)
```

## 10. Conditional Statements

### If-Else

```python
if age >= 18:
    print("Adult")
elif age >= 13:
    print("Teenager")
else:
    print("Child")
```

### Ternary Operator

```python
result = "Adult" if age >= 18 else "Minor"
```

### Match-Case (Python 3.10+)

```python
match day:
    case 1:
        print("Monday")
    case 2:
        print("Tuesday")
    case _:
        print("Invalid day")
```

## 11. Loops

```python
# For loop
for i in range(5):
    print(i)

# While loop
while age < 25:
    age += 1

# Iterate through a list
for item in numbers:
    print(item)

# Enumerate
for index, value in enumerate(numbers):
    print(index, value)
```

- `break` — Exit the loop.
- `continue` — Skip the current iteration.
- `pass` — Placeholder for an empty block.
- `range(start, stop, step)` — Generate a sequence of numbers.

## 12. Functions

### Function Definition

```python
def greet(name):
    return f"Hello, {name}"

greet("Alex")
```

### Default Parameters

```python
def greet(name="Guest"):
    print(f"Hello, {name}")
```

### Keyword & Variable Arguments

```python
def student(name, age):
    print(name, age)

student(age=22, name="Alex")

def add(*numbers):
    return sum(numbers)

def details(**data):
    print(data)
```

- `*args` — Accepts multiple positional arguments.
- `**kwargs` — Accepts multiple keyword arguments.
- `return` — Returns a value from a function.

## 13. Lambda Functions

Small anonymous functions.

```python
square = lambda x: x * x

add = lambda a, b: a + b

print(square(5))
```

## 14. Object-Oriented Programming (OOP)

### Classes & Objects

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def introduce(self):
        print(self.name, self.age)

student = Student("Alex", 22)
student.introduce()
```

### Inheritance

```python
class Animal:
    def sound(self):
        print("Animal sound")

class Dog(Animal):
    def bark(self):
        print("Bark")
```

### Polymorphism

```python
class Dog:
    def sound(self):
        print("Bark")

class Cat:
    def sound(self):
        print("Meow")

for animal in [Dog(), Cat()]:
    animal.sound()
```

### Encapsulation

```python
class Person:
    def __init__(self, name):
        self.__name = name

    def get_name(self):
        return self.__name
```

### Class & Static Methods

```python
class Example:
    @classmethod
    def class_method(cls):
        pass

    @staticmethod
    def static_method():
        pass
```

## 15. Exception Handling

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero")
else:
    print("Success")
finally:
    print("Execution completed")
```

### Raise an Exception

```python
if age < 18:
    raise ValueError("Age must be 18 or above")
```

## 16. File Handling

### Read a File

```python
with open("file.txt", "r") as file:
    content = file.read()
```

### Write a File

```python
with open("file.txt", "w") as file:
    file.write("Hello Python")
```

### Append to a File

```python
with open("file.txt", "a") as file:
    file.write("\nNew line")
```

**File Modes**

| Mode | Description |
|---|---|
| `r` | Read |
| `w` | Write (overwrites existing content) |
| `a` | Append |
| `x` | Create a new file |
| `b` | Binary mode |

## 17. Modules & Packages

```python
import math
import random

from datetime import datetime
from math import sqrt

math.sqrt(25)
random.randint(1, 10)
datetime.now()
```

### Create Your Own Module

```python
# calculator.py
def add(a, b):
    return a + b

# main.py
import calculator

calculator.add(10, 20)
```

## 18. Useful Built-in Functions

| Function | Description |
|---|---|
| `len()` | Get length |
| `type()` | Check data type |
| `range()` | Generate a sequence |
| `sum()` | Calculate total |
| `min()` | Get minimum value |
| `max()` | Get maximum value |
| `sorted()` | Return a sorted list |
| `reversed()` | Return a reverse iterator |
| `enumerate()` | Get index and value |
| `zip()` | Combine iterables |
| `map()` | Apply a function to elements |
| `filter()` | Filter elements |
| `any()` | Check if any element is true |
| `all()` | Check if all elements are true |
| `isinstance()` | Check object type |

## 19. Useful Python Concepts

- `self` — Refers to the current object.
- `__init__()` — Initializes an object.
- `__name__` — Special module variable.
- `if __name__ == "__main__":` — Runs code only when the file is executed directly.
- `None` — Represents the absence of a value.
- `pass` — Empty placeholder statement.
- `del` — Delete a variable or object reference.
- `with` — Manages resources automatically.
- `global` — Access or modify a global variable.
- `nonlocal` — Refer to a variable in an enclosing function.

### Main Guard

```python
def main():
    print("Hello Python")

if __name__ == "__main__":
    main()
```

## 20. Common Python Commands

```bash
python --version          # Check Python version
python main.py            # Run Python file
python -m pip install requests   # Install package
python -m pip list        # List installed packages
python -m pip uninstall requests # Remove package
python -m venv venv       # Create virtual environment
```

### Virtual Environment

```bash
# Activate (Linux / macOS)
source venv/bin/activate

# Activate (Windows)
venv\Scripts\activate

# Deactivate
deactivate
```

## 21. Quick Revision

- Use meaningful variable names and proper indentation.
- Understand lists, tuples, sets and dictionaries.
- Learn list and dictionary comprehensions.
- Understand functions, `*args` and `**kwargs`.
- Practice OOP concepts and inheritance.
- Use `try...except` for error handling.
- Use `with open()` for file handling.
- Learn modules, packages and virtual environments.
