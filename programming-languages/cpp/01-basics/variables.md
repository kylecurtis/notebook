# Variables and Constants in C++

<br>

## Variable Assignment and Initialization

Initialization is the process of assigning an initial value to a variable when
it's declared. Modern C++ encourages using direct-list or value initialization
because they work consistently across different types, help prevent errors, and
provide a clear initialization pattern.

<br>

## Forms of Initialization

| Form                        | Syntax Example | Description                                                                                                           |
| --------------------------- | -------------- | --------------------------------------------------------------------------------------------------------------------- |
| Default Initialization      | `int a;`       | Declares a variable without an explicit initializer. For fundamental types, the value remains indeterminate (unsafe). |
| Copy Initialization         | `int b = 5;`   | Uses the equals sign to initialize with a copy of the provided value.                                                 |
| Direct Initialization       | `int c(5);`    | Uses parentheses to directly initialize the variable.                                                                 |
| List Initialization         | `int d{5};`    | Uses braces to initialize. Prevents narrowing conversions and works consistently across all types.                    |
| Value (Zero) Initialization | `int e{};`     | Ensures initialization to a default value (zero for fundamental types).                                               |

<br>

### Default Initialization

Default initialization leaves fundamental types with unpredictable values, which
can lead to bugs if used before assignment.

```cpp
int a;  // Value is indeterminate - could contain any value
```

<br>

### Copy Initialization

This traditional form is easy to read but may hide implicit conversions.

```cpp
int b = 5;  // b is initialized to 5
```

<br>

### Direct Initialization

Makes initialization explicit and directly invokes constructors for user-defined
types.

```cpp
int c(5);  // c is initialized to 5
```

<br>

### List Initialization (Modern C++)

```cpp
int d{5};  // d is initialized to 5
```

<br>

Introduced in C++11, this form prevents narrowing conversions:

```cpp
int x{4.5};  // Error: narrowing conversion
int y = 4.5; // No error: silently truncates to 4
```

<br>

### Value (Zero) Initialization

Guarantees variables start with a known "zero" state.

```cpp
int e{};     // e is initialized to 0
int f = int(); // f is also initialized to 0
```

<br>

## Constants in C++

C++ offers several ways to define constants, each with different characteristics
and use cases.

<br>

### const

The `const` keyword creates a value that cannot be modified after
initialization.

```cpp
const int maxScore{100};  // Cannot be changed later
maxScore = 200;  // Compilation error
```

Key characteristics:

-   Can be initialized at runtime
-   The value cannot be changed after initialization
-   Can be used for variables whose value is determined during execution

<br>

### constexpr (C++11)

The `constexpr` keyword indicates that a value can be computed at compile time.

```cpp
constexpr int daysInWeek{7};  // Evaluated at compile time
```

Key characteristics:

-   Must be initialized with a value that can be determined at compile time
-   Enables compiler optimizations
-   Can be used in contexts requiring compile-time constants (like array sizes)

```cpp
constexpr int square(int x) {
    return x * x;
}

constexpr int result{square(5)};  // Computed at compile time
```

<br>

### constinit (C++20)

The `constinit` keyword ensures that a variable has static initialization
(initialized at compile time).

```cpp
constinit static int counter{0};  // Guaranteed compile-time initialization
```

Key characteristics:

-   Ensures initialization happens at compile time
-   Unlike const, allows the value to be modified later
-   Only applies to variables with static or thread storage duration

```cpp
constinit static int value{42};  // Initialized at compile time
value = 100;  // Valid - value can be changed
```

<br>

## Differences Between const, constexpr, and constinit

| Feature                 | const                | constexpr                            | constinit                        |
| ----------------------- | -------------------- | ------------------------------------ | -------------------------------- |
| When introduced         | C++ beginning        | C++11                                | C++20                            |
| Modifiable after init   | No                   | No                                   | Yes                              |
| Compile-time evaluation | Not required         | Required                             | Required for initialization only |
| Purpose                 | Prevent modification | Optimize for compile-time evaluation | Ensure static initialization     |

<br>

## Modern C++ Best Practices

-   **Use List Initialization (`{}`)**: Works consistently and prevents narrowing conversions
-   **Initialize Variables at Declaration**: Avoid uninitialized variables
-   **Prefer `constexpr` Over `const`**: When the value is known at compile time
-   **Use `const` for Values That Shouldn't Change**: Makes code more predictable
-   **Consider `constinit` for Static Variables**: Prevents the static initialization order fiasco

<br>

## Simple Example Using All Concepts

```cpp
#include <iostream>

// Compile-time constant - can be used for array sizes, etc.
constexpr int maxPlayers{4};

// Function that can be evaluated at compile time
constexpr int multiply(int a, int b) {
    return a * b;
}

int main() {
    // List initialization with a compile-time expression
    int scores[maxPlayers]{};  // All initialized to 0

    // Regular constant - cannot be modified
    const int gameLevel{5};

    // Compile-time computed value
    constexpr int timeLimit{multiply(gameLevel, 10)};

    // Variable that can change
    int currentScore{0};
    currentScore = 10;  // Valid - not a constant

    return 0;
}
```
