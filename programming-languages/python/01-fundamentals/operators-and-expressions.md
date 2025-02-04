## Overview

Operators in Python allow you to perform various computations and logical operations. Expressions are combinations of values, variables, and operators that produce a new value when evaluated. This guide covers arithmetic, comparison, logical, and bitwise operators, explains operator precedence and associativity, and discusses expression evaluation and short-circuiting.

<br>

---

<br>

## Arithmetic Operators

Arithmetic operators perform mathematical calculations on numeric values. The primary arithmetic operators include addition (+), subtraction (-), multiplication (\*), division (/), floor division (//), modulus (%), and exponentiation (\*\*).

Example:

```python
a = 10
b = 3

sum_result = a + b        # 13
difference = a - b        # 7
product = a * b           # 30
quotient = a / b          # 3.333...
floor_div = a // b        # 3 (division rounded down)
remainder = a % b         # 1 (modulus operation)
power = a ** b            # 10 raised to the power of 3 -> 1000
```

<br>

---

<br>

## Comparison Operators

Comparison operators are used to compare two values. They return a Boolean value (True or False). The common comparison operators include:

- Equal to (\=\=)
- Not equal to (!=)
- Greater than (>)
- Less than (<)
- Greater than or equal to (>=)
- Less than or equal to (<=)

Example:

```python
x = 5
y = 10

print(x == y)    # False
print(x != y)    # True
print(x < y)     # True
print(x > y)     # False
print(x <= 5)    # True
print(y >= 10)   # True
```

<br>

---

<br>

## Logical Operators

Logical operators combine Boolean values. The primary logical operators are:

- And (and)
- Or (or)
- Not (not)

These operators are used to create compound conditions.

Example:

```python
a = True
b = False

result_and = a and b   # False: both must be True for the result to be True
result_or = a or b     # True: at least one is True
result_not = not a     # False: negates the boolean value
```

<br>

---

<br>

## Bitwise Operators

Bitwise operators work on the binary representation of integers. They include:

- AND (&): Performs a bitwise AND.
- OR (|): Performs a bitwise OR.
- XOR (^): Performs a bitwise exclusive OR.
- NOT (~): Inverts the bits.
- Left Shift (<<): Shifts bits to the left.
- Right Shift (>>): Shifts bits to the right.

Example:

```python
x = 10   # In binary: 1010
y = 4    # In binary: 0100

bitwise_and = x & y   # 0 (binary 0000)
bitwise_or = x | y    # 14 (binary 1110)
bitwise_xor = x ^ y   # 14 (binary 1110)
bitwise_not = ~x      # -11 (inversion of 1010 gives ...0101 in two's complement)
left_shift = x << 1   # 20 (binary: 10100)
right_shift = x >> 1  # 5 (binary: 0101)
```

<br>

---

<br>

## Operator Precedence and Associativity

Operator precedence determines the order in which operations are evaluated in an expression. Operators with higher precedence are evaluated before operators with lower precedence. Associativity defines the order in which operators of the same precedence level are processed (left-to-right or right-to-left).

Some key points include:

- Parentheses have the highest precedence. They can be used to explicitly control the order of evaluation.
- Exponentiation (\*\*) has right-to-left associativity.
- Multiplication, division, floor division, and modulus share the same level of precedence and are evaluated left-to-right.
- Addition and subtraction are evaluated after multiplication and division, also left-to-right.
- Comparison operators are evaluated after arithmetic operators.
- Logical operators have the lowest precedence, with "not" evaluated before "and" and "or".

Example:

```python
# Multiplication is performed before addition, result is 11
result = 3 + 4 * 2

# Parentheses alter the order, result is 14
result_with_parentheses = (3 + 4) * 2

# Exponentiation associativity:
exp_result = 2 ** 3 ** 2  # Evaluated as 2 ** (3 ** 2), which is 2 ** 9 = 512
```

<br>

---

<br>

## Expression Evaluation and Short-Circuiting

Expression evaluation in Python follows the operator precedence and associativity rules. When evaluating logical expressions, Python employs short-circuiting. This means that evaluation stops as soon as the outcome is determined.

For example:

- In an "and" expression, if the first operand evaluates to False, the overall expression is False and the second operand is not evaluated.
- In an "or" expression, if the first operand evaluates to True, the overall expression is True and the second operand is not evaluated.

Example:

```python
def func():
    print("Function was called")
    return True

# Short-circuiting with 'and'
result = False and func()  # func() is not called because the first operand is False

# Short-circuiting with 'or'
result = True or func()    # func() is not called because the first operand is True
```

Short-circuiting is beneficial for performance and is often used to prevent errors, such as avoiding a function call that might raise an exception if its input is not valid.