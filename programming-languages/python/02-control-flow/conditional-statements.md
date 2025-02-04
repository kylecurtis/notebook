## Conditional Statements

> Conditional statements allow you to control the flow of your Python programs by executing code based on certain conditions. This guide covers traditional conditional statements (if, elif, else), ternary operators (conditional expressions), and the pattern matching feature introduced in Python 3.10.

<br>

---

<br>

## if, elif, else

> The most common form of conditional statements in Python uses the keywords `if`, `elif`, and `else` to execute code blocks based on whether a condition evaluates to True or False.

<br>

**Example:**

```python
x = 10

if x > 10:
    print("x is greater than 10")
elif x == 10:
    print("x is equal to 10")
else:
    print("x is less than 10")
```

<br>

**Key Points:**

- The `if` statement checks the first condition.
- The `elif` (short for "else if") statements allow you to check additional conditions.
- The `else` statement executes if none of the previous conditions are True.
- Only one block of code is executed: the first one with a condition that evaluates to True.

<br>

---

<br>

## Ternary Operators and Conditional Expressions

> A ternary operator in Python provides a compact syntax for choosing between two values based on a condition. This is also known as a conditional expression.

<br>

**Syntax:**

```
value_if_true if condition else value_if_false
```

<br>

**Example:**

```python
x = 5
result = "Positive" if x > 0 else "Non-positive"
print(result)  # Outputs: Positive
```

<br>

**Usage Notes:**

- Ternary operators are best used for simple, single-line conditions.
- They can help make the code more concise but should be used carefully to maintain readability.

<br>

---

<br>

## Pattern Matching (Python 3.10+)

> Python 3.10 introduced structural pattern matching, which offers a powerful and flexible way to compare values against patterns. This feature resembles switch/case statements found in other languages but is more advanced.

<br>

**Basic Syntax:**

```python
def process_value(value):
    match value:
        case 1:
            return "One"
        case 2:
            return "Two"
        case _:
            return "Something else"

result = process_value(2)
print(result)  # Outputs: Two
```

<br>

**Key Points:**

- The `match` statement is followed by a subject expression.
- The `case` clauses are used to specify different patterns to match against the subject.
- The underscore `_` is a wildcard pattern that matches any value and is typically used as a default case.
- Patterns can include literal values, variable capture, sequence patterns, mapping patterns, and even class patterns.

<br>

**Advanced Example with Pattern Matching:**

```python
def http_status(status):
    match status:
        case 200:
            return "OK"
        case 400:
            return "Bad request"
        case 404:
            return "Not found"
        case 500:
            return "Internal server error"
        case _:
            return "Unknown status"

print(http_status(404))  # Outputs: Not found
```

<br>

**Usage Notes:**

- Pattern matching can simplify complex conditionals and improve code readability.
- It supports deep matching on structured data such as lists, dictionaries, and custom classes.
- Use pattern matching when you have multiple conditions that compare the same subject or when you want to destructure data directly in the condition.