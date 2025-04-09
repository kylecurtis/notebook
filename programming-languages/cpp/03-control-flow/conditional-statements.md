# Conditional Statements in C++

Conditional statements allow programs to execute different code paths based on specific conditions. C++ offers several mechanisms for implementing conditionals, from basic if statements to more specialized constructs.

```cpp
#include <iostream> // For input/output operations
#include <string> // For string operations
#include <vector> // For vector container
#include <cstdint> // For fixed-width integer types
#include <type_traits> // For type traits used in constexpr if examples
```

## if Statements

The most basic form of conditional statement, executing code only when a condition evaluates to true.

### Simple if

```cpp
int temperature{31};

if (temperature > 30) {
    std::cout << "It's hot outside.\n";
}

// Single-statement if can omit braces (not recommended for readability)
if (temperature > 40)
    std::cout << "Extreme heat warning.\n";
```

### if-else

Provides an alternative execution path when the condition is false.

```cpp
int score{85};

if (score >= 60) {
    std::cout << "You passed.\n";
} else {
    std::cout << "You failed.\n";
}
```

### if-else if-else Chains

Allows checking multiple conditions in sequence.

```cpp
int grade{75};

if (grade >= 90) {
    std::cout << "A grade\n";
} else if (grade >= 80) {
    std::cout << "B grade\n";
} else if (grade >= 70) {
    std::cout << "C grade\n";
} else if (grade >= 60) {
    std::cout << "D grade\n";
} else {
    std::cout << "F grade\n";
}
```

### Nested if Statements

Conditional statements inside other conditional statements.

```cpp
bool isLoggedIn{true};
bool isAdmin{false};
bool hasPermission{true};

if (isLoggedIn) {
    if (isAdmin) {
        std::cout << "Admin dashboard\n";
    } else {
        if (hasPermission) {
            std::cout << "User dashboard with extra features\n";
        } else {
            std::cout << "Basic user dashboard\n";
        }
    }
} else {
    std::cout << "Please log in\n";
}
```

## switch Statements

Provides multi-way branching based on the value of an integral or enumeration expression.

### Case Labels and break

```cpp
int dayOfWeek{3}; // 1 = Monday, ..., 7 = Sunday

switch (dayOfWeek) {
    case 1:
        std::cout << "Monday\n";
        break;
    case 2:
        std::cout << "Tuesday\n";
        break;
    case 3:
        std::cout << "Wednesday\n";
        break;
    case 4:
        std::cout << "Thursday\n";
        break;
    case 5:
        std::cout << "Friday\n";
        break;
    case 6:
        std::cout << "Saturday\n";
        break;
    case 7:
        std::cout << "Sunday\n";
        break;
}
```

### Default Case

Executes when no case matches the switch expression.

```cpp
int errorCode{404};

switch (errorCode) {
    case 200:
        std::cout << "OK\n";
        break;
    case 404:
        std::cout << "Not Found\n";
        break;
    case 500:
        std::cout << "Server Error\n";
        break;
    default:
        std::cout << "Unknown Error\n";
        break;
}
```

### Fall-through Behavior

Without `break`, execution continues to the next case.

```cpp
int month = 7; // July
bool isLeapYear = false;

std::cout << "Days in month: ";
switch (month) {
    case 2: // February
        if (isLeapYear)
            std::cout << "29\n";
        else
            std::cout << "28\n";
        break;
    case 4: // April
    case 6: // June
    case 9: // September
    case 11: // November
        std::cout << "30\n";
        break;
    default: // All other months
        std::cout << "31\n";
        break;
}
```

### Switch on Strings (Implementation Techniques)

C++ doesn't directly support switching on strings, but there are workarounds.

```cpp
// Option 1: Use if-else chains
std::string command = "open";

if (command == "open") {
    // Handle open
} else if (command == "save") {
    // Handle save
} else if (command == "quit") {
    // Handle quit
}
```

```cpp
// Option 2: Use a map (more efficient for many cases)
#include <map>
#include <functional>

std::map<std::string, std::function<void()>> commandMap = {
    {"open", []() { std::cout << "Opening file\n"; }},
    {"save", []() { std::cout << "Saving file\n"; }},
    {"quit", []() { std::cout << "Quitting application\n"; }}
};

// Usage
auto it = commandMap.find(command);
if (it != commandMap.end()) {
    it->second(); // Execute the function
}
```

```cpp
// Option 3: Use string hashing
#include <functional>

// Get a hash at compile time if possible
constexpr uint32_t hash(const char* str) {
    uint32_t h = 0;
    while (*str) {
        h = h * 101 + *str++;
    }
    return h;
}

uint32_t cmdHash = std::hash<std::string>{}(command);

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

### Switch on Class Types (Implementation Techniques)

Similar to strings, C++ doesn't directly support switching on class types.

```cpp
// Option 1: Use type codes in classes
class Shape {
public:
    enum class Type { Circle, Rectangle, Triangle };
    virtual Type getType() const = 0;
};

class Circle : public Shape {
public:
    Type getType() const override { return Type::Circle; }
};

// Usage
Shape* shape = new Circle();
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
```

```cpp
// Option 2: Use dynamic_cast for type checking
if (auto* circle = dynamic_cast<Circle*>(shape)) {
    // Handle circle
} else if (auto* rectangle = dynamic_cast<Rectangle*>(shape)) {
    // Handle rectangle
} else if (auto* triangle = dynamic_cast<Triangle*>(shape)) {
    // Handle triangle
}
```

```cpp
// Option 3: Using visitor pattern (advanced)
class ShapeVisitor {
public:
    virtual void visit(Circle& circle) = 0;
    virtual void visit(Rectangle& rectangle) = 0;
    virtual void visit(Triangle& triangle) = 0;
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

A ternary operator providing a compact way to express simple conditionals.

```cpp
int age{20};
std::string status = (age >= 18) ? "adult" : "minor";

// Equivalent if-else
std::string statusIfElse;
if (age >= 18) {
    statusIfElse = "adult";
} else {
    statusIfElse = "minor";
}

// Useful for conditional initialization
int value{42};
int absValue = (value < 0) ? -value : value;

// Used in return statements
bool isEven(int num) {
    return (num % 2 == 0) ? true : false;
    // Or simply: return (num % 2 == 0);
}
```

### Nested Conditional Operators

Can be nested, but may reduce readability.

```cpp
int score{85};
char grade = (score >= 90) ? 'A' : 
             (score >= 80) ? 'B' : 
             (score >= 70) ? 'C' : 
             (score >= 60) ? 'D' : 'F';

// More readable with parentheses
int x = 1, y = 2, z = 3;
int smallest = (x < y) ? ((x < z) ? x : z) : ((y < z) ? y : z);
```

### Return Value Restrictions

Both expressions must be convertible to a common type.

```cpp
// Both branches must have compatible types
// int n = (condition) ? "string" : 42;  // Error: incompatible types

// Works with compatible types
double result = (x > 0) ? x : 3.14;  // int and double -> double

// Both branches are evaluated for type compatibility, but only the
// selected branch is executed
int divisor = 0;
double result = (divisor != 0) ? (100.0 / divisor) : 0.0;  // Safe, no division by zero
```

## C++17 Enhancements

C++17 added new forms of conditional statements with built-in initialization.

### if with Initialization (C++17)

Allows declaring a variable within the if statement.

```cpp
// Traditional approach
{
    auto result = functionCall();
    if (result.success) {
        // Use result
    }
}

// C++17 approach: init + condition
if (auto result = functionCall(); result.success) {
    // Use result
    // result is scoped to this if block and any else blocks
}

// Also works with else
if (auto pos = text.find("key"); pos != std::string::npos) {
    std::cout << "Found at position " << pos << '\n';
} else {
    std::cout << "Not found\n";
}
```

### Benefits for Scope Control

Limits the scope of variables used only in the conditional.

```cpp
// Before C++17
{
    std::lock_guard<std::mutex> lock(mutex);
    if (resource.isAvailable()) {
        // Use resource
    }
} // lock is released here, even though we only need it for the check

// With C++17
if (std::lock_guard<std::mutex> lock(mutex); resource.isAvailable()) {
    // Use resource
    // lock scope is restricted to this block
}
```

### switch with Initialization (C++17)

Similar to if, but for switch statements.

```cpp
switch (int value = getValue(); value) {
    case 1:
        std::cout << "Value is 1\n";
        break;
    case 2:
        std::cout << "Value is 2\n";
        break;
    default:
        std::cout << "Value is " << value << '\n';
        break;
}
// value is no longer accessible here
```

## constexpr if (C++17)

Allows compile-time conditional compilation based on constant expressions.

### Compile-time Branching

```cpp
template <typename T>
auto getValue(T t) {
    if constexpr (std::is_integral_v<T>) {
        return t * 2; // Only compiled for integral types
    } else if constexpr (std::is_floating_point_v<T>) {
        return t * 2.5; // Only compiled for floating-point types
    } else {
        return t; // Only compiled for other types
    }
}

// Usage
int i = getValue(10);       // Returns 20
double d = getValue(10.0);  // Returns 25.0
std::string s = getValue(std::string("test"));  // Returns "test"
```

### Template Specialization Alternative

Replaces the need for some template specializations.

```cpp
// Before C++17: Multiple template specializations
template<typename T>
void process(T value) {
    // Default implementation
}

template<>
void process<int>(int value) {
    // Special handling for int
}

template<>
void process<double>(double value) {
    // Special handling for double
}

// With C++17 constexpr if: Single template
template<typename T>
void process(T value) {
    if constexpr (std::is_same_v<T, int>) {
        // Special handling for int
    } else if constexpr (std::is_same_v<T, double>) {
        // Special handling for double
    } else {
        // Default implementation
    }
}
```

## Advanced Conditional Techniques

### Short-circuit Evaluation in Conditionals

Logical operators `&&` and `||` evaluate only what's necessary.

```cpp
// && short-circuits: right operand is only evaluated if left is true
bool isValid = (ptr != nullptr) && (ptr->value > 0);

// || short-circuits: right operand is only evaluated if left is false
bool needsUpdate = isDirty || hasChanged();

// Common pattern for safe access
if (ptr != nullptr && ptr->isReady() && ptr->value > threshold) {
    // Safe to use ptr
}

// Short-circuit to avoid expensive computations
if (quickCheck() || expensiveCheck()) {
    // Do something
}

// Short-circuit to implement a default value
const std::string& name = getName().empty() ? "Default" : getName();
```

### Branch Prediction Optimization

Helps compiler optimize conditional code paths.

```cpp
#include <cstdlib>

// Using [[likely]] and [[unlikely]] attributes (C++20)
if (x > 0) [[likely]] {
    // This branch is more likely to be taken
    // Compiler optimizes for this path
} else {
    // Less common path
}

// Before C++20: Using compiler-specific builtin functions
if (__builtin_expect(x > 0, 1)) {  // GCC/Clang syntax, 1 means likely
    // More likely branch
} else {
    // Less likely branch
}

// Check that's almost always true
while (i < n) [[likely]] {
    // Loop body
    i++;
}
```

### Branchless Programming Techniques

Avoid branches for performance-critical code.

```cpp
// Using conditional operator for branchless code
int abs_branchy(int x) {
    if (x < 0)
        return -x;
    else
        return x;
}

int abs_branchless(int x) {
    int mask = x >> 31;  // All bits set to 1 if negative, 0 otherwise
    return (x + mask) ^ mask;  // Branchless absolute value
}

// Using bit manipulation for branchless max
int max_branchy(int a, int b) {
    if (a > b)
        return a;
    else
        return b;
}

int max_branchless(int a, int b) {
    return b + ((a - b) & -((a - b) >> 31));
}

// Using arithmetic for branchless operations
bool isEven_branchy(int x) {
    return (x % 2 == 0);
}

bool isEven_branchless(int x) {
    return !(x & 1);
}

// Lookup tables for branchless switches
const char* dayNames[] = {"Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"};
const char* getDayName(int day) {
    // Bounds checking can also be branchless with bit manipulation
    return dayNames[(day - 1) % 7];  // Assumes day is 1-7
}
```

## Best Practices

1. **Use braces** for all conditional blocks, even single statements, for clarity and to prevent bugs.
    
2. **Keep conditionals simple** - complex conditions should be broken down or extracted into named functions.
    
    ```cpp
    // Hard to understand:
    if (user.isActive() && (user.getRole() == "admin" || user.hasPermission("edit")) && !system.isInMaintenance()) {
        // ...
    }
    
    // Better:
    bool userCanEdit = user.isActive() && 
                       (user.getRole() == "admin" || user.hasPermission("edit"));
    bool systemIsReady = !system.isInMaintenance();
    
    if (userCanEdit && systemIsReady) {
        // ...
    }
    ```
    
3. **Favor `switch` over long `if-else` chains** when checking a single value against multiple constants.
    
4. **Always include a `default` case** in `switch` statements, even if empty, to handle unexpected values.
    
5. **Be cautious with fall-through** in `switch` statements - use `[[fallthrough]]` attribute (C++17) to indicate intentional fall-through.
    
    ```cpp
    switch (value) {
        case 1:
            // Do something
            [[fallthrough]]; // Explicitly shows intent to fall through
        case 2:
            // Do something more
            break;
    }
    ```
    
6. **Prefer initialization with `if` (C++17)** when the variable is only needed within the condition.
    
7. **Use `constexpr if` for template code** instead of template specialization when appropriate.
    
8. **Consider branchless programming** for performance-critical code, especially in tight loops.