# Conditional Statements in C++

Conditional statements allow programs to execute different code paths based on specific conditions. Modern C++ provides several mechanisms for conditionals—from fundamental `if` statements to specialized compile-time branches. This guide covers the core ideas for beginners and also serves as a reference for advanced techniques.

```cpp
#include <iostream> // For I/O
#include <string> // For std::string
#include <vector> // For std::vector
#include <cstdint> // For fixed-width integer types
#include <type_traits> // For type traits (used in constexpr if examples)
```

## Boolean Conversions in Conditions

- In C++, **zero (0)** or a **null pointer** is treated as `false`, while any **nonzero** or **non-null** value is treated as `true`.
    
- This means integer and pointer expressions can be used directly in conditionals. For clarity, prefer explicit comparisons (`value != 0`, `ptr != nullptr`) unless brevity is desired.
    

```cpp
int number{42};

if (number) { // Equivalent to (number != 0)
    std::cout << "Number is nonzero." << '\n';
}

if (!number) {
    std::cout << "Number is zero." << '\n';
}
```

## if Statements

### Simple if

Use `if` to execute code only when a condition is true.

```cpp
int temperature{31}; // Celsius

if (temperature > 30) { // Check if above 30
    std::cout << "It's hot outside." << '\n';
}

// Single-statement if without braces (less clear):
if (temperature > 40)
    std::cout << "Extreme heat warning." << '\n';
```

### if-else

Provide an alternative branch when the condition is false.

```cpp
int score{85}; // Example score

if (score >= 60) {
    std::cout << "You passed." << '\n';
} else {
    std::cout << "You failed." << '\n';
}
```

### if-else / else if Chains

Used to check multiple conditions in sequence.

```cpp
int grade{75}; // Example grade

if (grade >= 90) {
    std::cout << "A grade" << '\n';
} else if (grade >= 80) {
    std::cout << "B grade" << '\n';
} else if (grade >= 70) {
    std::cout << "C grade" << '\n';
} else if (grade >= 60) {
    std::cout << "D grade" << '\n';
} else {
    std::cout << "F grade" << '\n';
}
```

### Nested if Statements

Place `if` statements inside one another.

```cpp
bool isLoggedIn{true}; // Example login status
bool isAdmin{false}; // Example admin flag
bool hasPermission{true}; // Example permission flag

if (isLoggedIn) {
    if (isAdmin) {
        std::cout << "Admin dashboard" << '\n';
    } else {
        if (hasPermission) {
            std::cout << "User dashboard with extra features" << '\n';
        } else {
            std::cout << "Basic user dashboard" << '\n';
        }
    }
} else {
    std::cout << "Please log in" << '\n';
}
```

## switch Statements

A `switch` statement enables multi-way branching based on an integral, enumeration, or character expression.

### Strongly Typed Enumerations

- **Prefer** `enum class` over traditional `enum` for type safety and scoping.
    
- When using `enum class`, you must qualify cases with the enum name.
    
- Optionally, omit `default` to get compiler warnings for unhandled enumerators.
    

```cpp
enum class DayOfWeek { Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday };

DayOfWeek day{DayOfWeek::Wednesday};

switch (day) {
    case DayOfWeek::Monday:
        std::cout << "Monday" << '\n';
        break;
    case DayOfWeek::Tuesday:
        std::cout << "Tuesday" << '\n';
        break;
    case DayOfWeek::Wednesday:
        std::cout << "Wednesday" << '\n';
        break;
    case DayOfWeek::Thursday:
        std::cout << "Thursday" << '\n';
        break;
    case DayOfWeek::Friday:
        std::cout << "Friday" << '\n';
        break;
    case DayOfWeek::Saturday:
        std::cout << "Saturday" << '\n';
        break;
    case DayOfWeek::Sunday:
        std::cout << "Sunday" << '\n';
        break;
    // Note: If you omit 'default' here, some compilers can warn if a new enumerator isn't handled.
}
```

### Case Labels and break

```cpp
int dayOfWeek{3}; // 1 = Monday, ..., 7 = Sunday

switch (dayOfWeek) {
    case 1:
        std::cout << "Monday" << '\n';
        break;
    case 2:
        std::cout << "Tuesday" << '\n';
        break;
    case 3:
        std::cout << "Wednesday" << '\n';
        break;
    case 4:
        std::cout << "Thursday" << '\n';
        break;
    case 5:
        std::cout << "Friday" << '\n';
        break;
    case 6:
        std::cout << "Saturday" << '\n';
        break;
    case 7:
        std::cout << "Sunday" << '\n';
        break;
}
```

### Default Case

```cpp
int errorCode{404}; // Example HTTP error code

switch (errorCode) {
    case 200:
        std::cout << "OK" << '\n';
        break;
    case 404:
        std::cout << "Not Found" << '\n';
        break;
    case 500:
        std::cout << "Server Error" << '\n';
        break;
    default:
        std::cout << "Unknown Error" << '\n';
        break;
}
```

### Fall-through Behavior

```cpp
int month{7}; // July
bool isLeapYear{false};

std::cout << "Days in month: ";
switch (month) {
    case 2: // February
        if (isLeapYear) {
            std::cout << "29" << '\n';
        } else {
            std::cout << "28" << '\n';
        }
        break;
    case 4: // April
    case 6: // June
    case 9: // September
    case 11: // November
        std::cout << "30" << '\n';
        break;
    default:
        std::cout << "31" << '\n';
        break;
}
```

## Switch on Strings (Implementation Techniques)

C++ doesn't directly allow `switch` on `std::string`. You have several workarounds:

```cpp
// Option 1: Use if-else chains
std::string command{"open"};

if (command == "open") {
    // Handle open
} else if (command == "save") {
    // Handle save
} else if (command == "quit") {
    // Handle quit
}
```

```cpp
// Option 2: Use a map
#include <map>
#include <functional>

std::map<std::string, std::function<void()>> commandMap {
    {"open", []() { std::cout << "Opening file" << '\n'; }},
    {"save", []() { std::cout << "Saving file" << '\n'; }},
    {"quit", []() { std::cout << "Quitting application" << '\n'; }}
};

auto it = commandMap.find(command);
if (it != commandMap.end()) {
    it->second(); // Execute the stored function
}
```

```cpp
// Option 3: Use string hashing
#include <functional>

std::string cmd{"open"};
std::size_t cmdHash = std::hash<std::string>{}(cmd);

switch (cmdHash) {
    case std::hash<std::string>{}("open"):
        // Handle open
        break;
    case std::hash<std::string>{}("save"):
        // Handle save
        break;
    case std::hash<std::string>{}("quit"):
        // Handle quit
        break;
}
```

## Switch on Class Types (Implementation Techniques)

Similar story for class types: you cannot `switch` on them directly.

```cpp
// Option 1: Use a type code in the class
class Shape {
public:
    enum class Type { Circle, Rectangle, Triangle };
    virtual Type getType() const = 0;
};

class Circle : public Shape {
public:
    Type getType() const override {
        return Type::Circle;
    }
};

Shape* shape{new Circle{}};

switch (shape->getType()) {
    case Shape::Type::Circle:
        // Handle circle
        break;
    case Shape::Type::Rectangle:
        // Handle rectangle
        break;
    case Shape::Type::Triangle:
        // Handle triangle
        break;
}

// Option 2: Use dynamic_cast
if (auto* circle = dynamic_cast<Circle*>(shape)) {
    // Handle circle
} else if (auto* rectangle = dynamic_cast<Rectangle*>(shape)) {
    // Handle rectangle
}

// Option 3: Visitor pattern
class ShapeVisitor {
public:
    virtual void visit(class Circle& c) = 0;
    virtual void visit(class Rectangle& r) = 0;
    virtual void visit(class Triangle& t) = 0;
};

class Shape {
public:
    virtual void accept(ShapeVisitor& visitor) = 0;
};

class Circle : public Shape {
public:
    void accept(ShapeVisitor& visitor) override {
        visitor.visit(*this);
    }
};
```

## Conditional Operator (?:)

The ternary operator offers concise expression-based conditionals.

```cpp
int age{20};
std::string status = (age >= 18) ? "adult" : "minor";

bool isEven(int num) {
    return (num % 2 == 0) ? true : false; // or just (num % 2 == 0)
}
```

### Nested Conditional Operators

```cpp
int score{85};
char grade = (score >= 90) ? 'A' :
             (score >= 80) ? 'B' :
             (score >= 70) ? 'C' :
             (score >= 60) ? 'D' : 'F';
```

### Return Value Restrictions

Both branches must have compatible types.

```cpp
// int and double -> result is double
double result = (x > 0) ? x : 3.14;
```

## C++17 Enhancements

### if with Initialization

Declare a variable inside the condition.

```cpp
if (auto result = functionCall(); result.success) {
    // Use result here
} else {
    // result is still in scope here
}
```

### switch with Initialization

```cpp
switch (int value = getValue(); value) {
    case 1:
        std::cout << "Value is 1" << '\n';
        break;
    default:
        // ...
        break;
}
```

## constexpr if (C++17)

Compile-time branching for templated code.

```cpp
template <typename T>
auto getValue(T t) {
    if constexpr (std::is_integral_v<T>) {
        return t * 2; // Only for integral types
    } else if constexpr (std::is_floating_point_v<T>) {
        return t * 2.5; // Only for floating-point types
    } else {
        return t; // All other types
    }
}
```

## Advanced Conditional Techniques

### Short-circuit Evaluation

Logical `&&` and `||` skip evaluating the right side if not necessary.

```cpp
if ((ptr != nullptr) && (ptr->value > 0)) {
    // Safe
}

bool needsUpdate = isDirty || hasChanged();
```

### Branch Prediction Optimization

Hints to the compiler which branch is likely.

```cpp
if (x > 0) [[likely]] {
    // More likely path
} else {
    // Less likely path
}
```

### Branchless Programming

Use bitwise/arithmetic operations instead of branching.

```cpp
int abs_branchless(int x) {
    int mask = x >> 31; // negative -> all bits = 1
    return (x + mask) ^ mask;
}
```

## Common Pitfalls

1. **Missing `break`** in `switch` causing unintentional fall-through.
    
2. **Using `=` instead of `==`** in conditionals.
    
3. **Omitting braces** for multi-line blocks, leading to logic errors.
    
4. **Confusing `&` with `&&`** or `|` with `||`.
    

## Real-World Use Cases

### Guard Clauses

Break out of a function early if conditions aren’t met.

```cpp
bool loadData(const std::string& filePath) {
    if (filePath.empty()) {
        std::cerr << "No file path provided" << '\n';
        return false;
    }
    // Perform load...
    return true;
}
```

### Separate Variables for Readability

```cpp
bool isUserActive = user.isActive();
bool canUserEdit = (user.isAdmin() || user.hasPermission("edit"));

if (isUserActive && canUserEdit && !system.isInMaintenance()) {
    // Proceed
}
```

## Best Practices

1. **Use braces** for clarity, even in single-line `if` or loops.
    
2. **Prefer `enum class`** over unscoped `enum`, especially in `switch`.
    
3. **Limit complexity** of conditionals; factor out complex logic into small functions or well-named local variables.
    
4. **Consider `switch`** for multiple comparisons on the same variable.
    
5. **Include a `default` case** in `switch` for robustness (or omit intentionally in `enum class` to catch unhandled values).
    
6. **Use C++17 `if`/`switch` init** to localize variables.
    
7. **Use `constexpr if`** for compile-time branching.
    
8. **Explore branchless techniques** in performance-critical code.
    
9. **Be mindful of short-circuiting** and potential side effects in expressions.
    