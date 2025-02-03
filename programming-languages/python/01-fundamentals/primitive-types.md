## Overview

- **Definition:** Primitive data types are the basic building blocks in Python. They represent simple values and are immutable (i.e., they cannot be changed after creation).

- **Key Types Covered:**
  - **Numbers:** Integers, floating-point numbers, and complex numbers.
  - **Strings:** Sequences of characters.
  - **Booleans:** Represent truth values (`True` and `False`).

> _Note:_ While the concept of type conversion is important, we’ll focus on core definitions and usage now. Type conversions will be explored in a later section.

<br>

---

<br>

## Numbers

<br>

### Integers (`int`)

- **Definition:** Whole numbers without a fractional component.
- **Syntax Examples:**

```python
a = 10
b = -5
c = 0
```

<br>

**Key Points:**

- Integers in Python have arbitrary precision (they can grow as large as memory allows).
- Use underscores for readability in large numbers:

```python
million = 1_000_000
```

<br>

**Common Operations:**

Arithmetic: `+`, `-`, `*`, `/`, `//` (floor division), `%` (modulus), `**` (exponentiation).

```python
x = 10
y = 3

print(x + y)   # 13
print(x - y)   # 7
print(x * y)   # 30
print(x / y)   # 3.3333333333333335
print(x // y)  # 3
print(x % y)   # 1
print(x ** y)  # 1000
```

<br>

Built-in functions: `abs()`, `pow()`, `divmod()`.

```python
print(abs(-42))       # 42
print(pow(2, 3))      # 8
print(divmod(10, 3))  # (3, 1)
```

<br>

---

<br>

### Floating-Point Numbers (`float`)

- **Definition:** Numbers with a fractional component.
- **Syntax Examples:**

```python
pi = 3.14159
negative = -0.001
```

<br>

**Key Points:**

- Floating-point arithmetic can introduce rounding errors; be cautious in financial or precision-critical applications.
- Python uses the double-precision (64-bit) format by default.

<br>

**Common Operations:**

- Standard arithmetic operations work similarly to integers.
- Functions: `round()`, `math.floor()`, `math.ceil()` (requires importing `math`).

```python
import math
print(round(pi, 2))      # 3.14
print(math.floor(pi))    # 3
print(math.ceil(pi))     # 4
```

<br>

---

<br>

### Complex Numbers (`complex`)

- **Definition:** Numbers with a real and an imaginary part.
- **Syntax Examples:**

```python
z1 = 2 + 3j
z2 = complex(2, -3)
```

<br>

**Key Points:**

- Useful in fields such as engineering and signal processing.
- Access real and imaginary parts via `.real` and `.imag`:

```python
print(z1.real)  # 2.0
print(z1.imag)  # 3.0
```

<br>

**Operations:**

- Standard arithmetic applies.
- Conjugate: use `.conjugate()`

```python
print(z1.conjugate())  # (2-3j)
```

<br>

---

<br>

## Strings

<br>

### String Literals

- **Definition:** A sequence of characters enclosed in quotes.
- **Types of Quotes:**
  - Single quotes: `'Hello'`
  - Double quotes: `"World"`
  - Triple quotes for multi-line strings:

```python
multi_line = """This is a
multi-line string."""
```

<br>

**Key Points:**

- Strings are immutable: any operation that appears to modify a string actually creates a new one.
- For special characters, use escape sequences (e.g., `\n` for newline, `\\` for a literal backslash).

<br>

### String Operations and Methods

<br>

**Concatenation:**

```python
greeting = "Hello, " + "World!"
```

<br>

**Repetition:**

```python
echo = "Hi! " * 3  # "Hi! Hi! Hi! "
```

<br>

**Indexing and Slicing:**

```python
s = "Python"
print(s[0])      # 'P'
print(s[-1])     # 'n'
print(s[1:4])    # 'yth'
```

<br>

**Common Methods:**

- `.upper()`, `.lower()`, `.strip()`, `.split()`, `.replace()`, `.find()`

```python
text = "   Hello, Python!   "
print(text.strip())         # "Hello, Python!"
print(text.replace("Python", "World"))
print(text.split(","))      # Splits into list based on delimiter
```

<br>

- **Formatting Strings:**

> f-Strings (Python 3.6+):

```python
name = "Alice"
age = 30
print(f"{name} is {age} years old.")
```

<br>

`str.format()` method:

```python
print("{} is {} years old.".format(name, age))
```

<br>

---

<br>

## Booleans

<br>

### Boolean Values

- **Definition:** Represent truth values—`True` and `False`.
- **Usage:**
  - Often used in conditional statements and logical operations.
  - Booleans are a subclass of integers: `True` is equivalent to `1`, and `False` is equivalent to `0`.

```python
print(True + True)   # 2
print(False * 10)    # 0
```

<br>

### Logical Operators

- **Operators:**
  - `and`, `or`, `not`
- **Examples:**

```python
a = True
b = False
print(a and b)  # False
print(a or b)   # True
print(not a)    # False
```

<br>

### Boolean Context

- **Truthiness:** Not only `True` or `False` are boolean values; many objects can be evaluated in a boolean context:
  - **Falsy values:** `False`, `None`, `0`, empty sequences/collections (e.g., `""`, `[]`, `{}`)
  - **Truthy values:** Non-zero numbers, non-empty sequences/collections.

```python
if []:
    print("This won't print because [] is falsy.")
else:
    print("Empty list is considered False.")
```
