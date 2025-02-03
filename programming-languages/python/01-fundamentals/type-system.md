## Overview of Python’s Type System

<br>

#### Dynamic Typing

Python uses dynamic typing, meaning that variables are not bound to a fixed type. The type is associated with the object the variable points to. For example, a variable can initially hold an integer and later be reassigned to a string.

```python
x = 10         # x is an int
x = "Python"   # Now, x is a str
```

<br>

#### Duck Typing

Python also follows the concept of duck typing. Duck typing in Python is a concept where the type of an object is less important than the methods and attributes it has. In other words, if an object "walks like a duck and quacks like a duck", it's treated as a duck, regardless of its actual type.

```python
def start_device(device):
    # This function expects that the 'device' has a 'start' method.
    device.start()

class Car:
    def start(self):
        print("The car engine starts.")

class Airplane:
    def start(self):
        print("The airplane's engines roar to life.")

# Instances of Car and Airplane
my_car = Car()
my_airplane = Airplane()

# Both work with start_device because they both have a start() method.
start_device(my_car)      # Outputs: The car engine starts.
start_device(my_airplane) # Outputs: The airplane's engines roar to life.
```

<br>

#### Static Type Hints

Static type hints were introduced in PEP 484. They help improve code readability and documentation and allow static analysis tools like mypy to catch type-related errors before runtime. These annotations do not affect runtime behavior.

```python
def greet(name: str) -> str:
    return f"Hello, {name}"
```

<br>

---

<br>

## Type Conversion (Casting)

Type conversion, or casting, is the process of converting values from one type to another. Python provides several built-in functions for these conversions.

<br>

To convert values to integers, use the `int()` function.

```python
a = int("123")   # Converts string to int -> 123
b = int(12.34)   # Converts float to int (truncates decimal) -> 12
```

<br>

To convert values to floating-point numbers, use the `float()` function.

```python
a = float("3.14")   # 3.14
b = float(10)       # 10.0
```

<br>

To convert values to strings, use the `str()` function. This converts any object to its string representation.

```python
a = str(123)      # "123"
b = str(3.14)     # "3.14"
c = str(True)     # "True"
```

<br>

To convert values to booleans, use the `bool()` function. Python determines the truthiness of a value based on its inherent properties.

```python
bool(0)       # False
bool(1)       # True
bool("")      # False (empty string is falsy)
bool("Hello") # True (non-empty string is truthy)
```

<br>

Conversion functions also work with collections and other types. For example, converting a string to a list of characters or converting a tuple to a list.

```python
s = "hello"
list_s = list(s)  # ['h', 'e', 'l', 'l', 'o']

t = (1, 2, 3)
list_t = list(t)  # [1, 2, 3]

tuple_list = tuple([1, 2, 3])  # (1, 2, 3)
set_list = set([1, 2, 2, 3])   # {1, 2, 3}
```

<br>

---

<br>

## Dynamic Typing vs. Duck Typing

Dynamic typing in Python means that types are checked at runtime. This allows variables to be reassigned to different types without causing errors.

```python
def add(a, b):
    return a + b

print(add(1, 2))         # 3 (works with integers)
print(add("foo", "bar")) # "foobar" (works with strings)
```

The advantage of dynamic typing is flexibility and rapid prototyping. However, it can lead to runtime errors if operations are performed on incompatible types.

<br>

Duck typing focuses on an object’s behavior rather than its explicit type. This means that if an object implements the required methods or attributes, it is acceptable regardless of its actual type.

```python
class Duck:
    def quack(self):
        print("Quack, quack!")

class Person:
    def quack(self):
        print("I'm imitating a duck!")

def make_it_quack(thing):
    thing.quack()  # Relies on the existence of quack()

d = Duck()
p = Person()
make_it_quack(d)  # Outputs: Quack, quack!
make_it_quack(p)  # Outputs: I'm imitating a duck!
```

When writing flexible functions, duck typing is a powerful approach. For cases where clarity is needed, explicit type checks (using `isinstance`) or static type hints can be used.

<br>

---

<br>

## Static Type Hints and mypy

Static type hints allow you to annotate your code with expected types. This helps improve clarity and enables static analysis tools like mypy to catch type mismatches before runtime.

You can annotate function parameters and return values as shown below:

```python
def multiply(a: int, b: int) -> int:
    return a * b
```

<br>

Variables can also be annotated with their expected types (as introduced in PEP 526):

```python
count: int = 10
name: str = "Alice"
```

<br>

For more complex types, the `typing` module provides support for collections and generics.

```python
from typing import List, Dict, Tuple, Optional

def process_items(items: List[str]) -> Dict[str, int]:
    return {item: len(item) for item in items}

def get_coordinates() -> Tuple[float, float]:
    return (40.7128, -74.0060)

def find_item(name: str) -> Optional[str]:
    items = ["apple", "banana", "cherry"]
    return name if name in items else None
```

<br>

To perform static type checking, install mypy using pip.

```bash
pip install mypy
```

<br>

Run mypy from the command line to check your file:

```bash
mypy your_script.py
```

<br>

Here is an example where mypy would catch a type error:

```python
# sample.py
def add(a: int, b: int) -> int:
    return a + b

result = add(1, "2")  # This should raise a type error with mypy.
```

Advanced type features include Union Types, Type Variables, Generics, and Callable types.

<br>

Union Types allow a variable or parameter to accept multiple types:

```python
from typing import Union

def stringify(num: Union[int, float]) -> str:
    return str(num)
```

<br>

Generics enable you to create functions and classes that operate on generic types:

```python
from typing import TypeVar, List

T = TypeVar('T')

def first_element(lst: List[T]) -> T:
    return lst[0]
```

<br>

Callable types specify the signature of a function expected as a parameter:

```python
from typing import Callable

def operate(func: Callable[[int, int], int], a: int, b: int) -> int:
    return func(a, b)
```

<br>

---

<br>

## Summary

Python’s dynamic typing allows for flexible and rapid development, but it can lead to runtime errors if not managed carefully. Duck typing encourages writing functions that operate on any object with the required behavior, regardless of its explicit type. Use built-in functions such as `int()`, `float()`, `str()`, and `bool()` for type conversion, and incorporate static type hints to enhance code clarity and robustness. Tools like mypy can then be used to catch type errors during development.
