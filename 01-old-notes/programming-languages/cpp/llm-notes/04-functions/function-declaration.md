# Function Declaration and Definition in C++

Functions are fundamental building blocks in C++, enabling modular, reusable, and well-organized code. This note covers the essential aspects of declaring and defining functions in C++.

```cpp
#include <iostream> // For standard I/O
#include <string> // For std::string
#include <vector> // For std::vector
#include <utility> // For std::move
```

---

## Function Syntax Elements

A typical function declaration includes:

- A return type
    
- A function name
    
- A parameter list (possibly empty or with default arguments)
    

```cpp
// Basic form
return_type function_name(parameter_type1 param1, parameter_type2 param2);

// Example
int calculateSum(int a, int b);

// With specifiers
inline constexpr int add(int a, int b) noexcept;
```

## Function Declarations vs Definitions

- **Declaration (prototype):** Specifies the function’s interface, typically placed in header files (`.h` / `.hpp`).
    
- **Definition:** Includes the function’s implementation, usually in `.cpp` files.
    

```cpp
// Declaration
double calculateArea(double length, double width);

// Definition
double calculateArea(double length, double width) {
    return length * width;
}

// Combined declaration & definition (often used for small functions)
int square(int x) {
    return x * x;
}
```

> **Note:** A non-inline function must be defined exactly once in the entire program.

---

## Return Types

Functions can return different kinds of values, depending on your design and performance needs.

### void Functions

`void` indicates no return value.

```cpp
void printMessage(const std::string& message) {
    std::cout << message << '\n';
}

void processCommand(const std::string& cmd) {
    if (cmd.empty()) {
        return; // Exit early
    }
    // Process command...
}
```

### Value Return Types

Functions returning a value by copy.

```cpp
int multiplyByTwo(int value) {
    return value * 2;
}

std::string createGreeting(const std::string& name) {
    return "Hello, " + name + "!";
}
```

Modern compilers optimize away unnecessary copies (Return Value Optimization).

### Reference Return Types

Returning a reference to an existing object. Be cautious never to return references to local variables.

```cpp
int& getElement(std::vector<int>& vec, size_t index) {
    return vec[index]; // References an existing element
}

// Example usage
std::vector<int> numbers = {10, 20, 30};
getElement(numbers, 1) = 25; // Changes the second element to 25
```

### Pointer Return Types

Returning a pointer to an object.

```cpp
int* findValue(std::vector<int>& vec, int target) {
    for (size_t i = 0; i < vec.size(); ++i) {
        if (vec[i] == target) {
            return &vec[i];
        }
    }
    return nullptr; // Not found
}

// Dynamically allocated pointer
int* createDynamicInt(int value) {
    return new int(value);
}
```

> **Important:** If you allocate memory inside a function, the caller must eventually free it.

### auto Return Type (C++14)

Type deduction for cleaner function signatures.

```cpp
auto add(int a, int b) {
    return a + b; // Deduces int
}

auto createPair(const std::string& key, int value) {
    return std::make_pair(key, value); // Deduces std::pair<std::string, int>
}
```

---

## Parameter Passing Mechanisms

How you pass parameters affects performance and the ability to modify outside data.

### Pass by Value

The function receives a copy of the argument.

```cpp
void incrementCopy(int value) {
    value++;
    // Only the local copy changes
}
```

### Pass by Reference

The function can modify the original argument.

```cpp
void increment(int& value) {
    value++;
}
```

### Pass by Constant Reference

Combines efficiency (no copy) with safety (no modification).

```cpp
void printDetails(const std::string& text) {
    std::cout << "Length: " << text.size() << " | " << text << '\n';
}
```

### Pass by Pointer

Useful for optional parameters (pointer can be `nullptr`).

```cpp
void modifyValue(int* ptr) {
    if (ptr) {
        (*ptr) *= 2;
    }
}
```

### Pass by Rvalue Reference

Enables _move semantics_, transferring resources efficiently.

```cpp
void processVector(std::vector<int>&& vec) {
    // Takes ownership of the vector
    vec.push_back(100);
}

std::vector<int> v = {1, 2, 3};
processVector(std::move(v)); // Moves from v
```

---

## Parameter Lists

### Empty Parameter Lists

A function can take no parameters:

```cpp
int getCurrentTime() {
    return static_cast<int>(time(nullptr));
}

void doNothing() {
    // ...
}
```

### void Parameter

Older style indicating no parameters:

```cpp
double getPi(void) {
    return 3.14159265359;
}
```

### Default Arguments

Provide a default value for parameters.

```cpp
void setConfiguration(bool logging = false, 
                      int cacheSize = 1024, 
                      const std::string& mode = "normal") {
    // ...
}

// Usage
setConfiguration();          // All defaults
setConfiguration(true);      // logging = true
setConfiguration(true, 2048, "enhanced");
```

> **Tip:** Place default arguments in the function declaration (often in the header).

### Variadic Functions (C-style)

Older approach for variable argument counts.

```cpp
#include <cstdarg>

int sum(int count, ...) {
    va_list args;
    va_start(args, count);
    
    int total = 0;
    for (int i = 0; i < count; ++i) {
        total += va_arg(args, int);
    }
    
    va_end(args);
    return total;
}
```

### Function Parameter Pack (C++11)

Type-safe, modern approach to variadic functions via templates.

```cpp
template<typename... Args>
void printAll(Args... args) {
    ((std::cout << args << ' '), ...); // Fold expression (C++17)
    std::cout << '\n';
}
```

---

## Function Signatures

A function’s **signature** includes its name and parameter types (the return type is _not_ part of the signature).

```cpp
void process(int value);
void process(double value);
// Different signatures

double calculate(int a, int b);
int calculate(int a, int b); // Error: same signature, conflicting return types
```

---

## Trailing Return Type Syntax (C++11)

Allows specifying the return type after the parameter list.

```cpp
// Traditional
int multiply(int a, int b);

// Trailing syntax
auto multiply(int a, int b) -> int;

// Useful with templates
template<typename T, typename U>
auto add(T a, U b) -> decltype(a + b) {
    return a + b;
}
```

---

## Linkage Specifications

### extern "C"

Specifies C linkage (no C++ name mangling), commonly used for C–C++ interoperability.

```cpp
extern "C" void cStyleFunction(int arg);

extern "C" {
    double calculateValue(double input);
    int processData(const char* data, size_t length);
}
```

### Language Linkage and ABI

Affects name mangling and calling conventions.

```cpp
// C++ linkage (default)
void cppFunction() { /* ... */ }

// C linkage
extern "C" void cFunction() { /* ... */ }
```

---

## Inline Functions

Suggests to the compiler that the function body should be expanded inline at the call site.

### inline Keyword

```cpp
inline int min(int a, int b) {
    return (a < b) ? a : b;
}

// Member functions defined inside a class are implicitly inline
class Example {
public:
    void method() {
        // ...
    }
};
```

### Compiler Inlining Decisions

`inline` is only a _request_—the compiler ultimately decides.

```cpp
inline int complexFunction(int x) {
    int result = 0;
    for (int i = 0; i < x; ++i) { 
        result += i * i; 
    }
    return result;
}
```

### Link-time Optimization

With LTO, compilers can make inlining decisions even across translation units.

---

## constexpr Functions (C++11)

### Rules and Restrictions

`constexpr` indicates a function can be evaluated at compile time (if provided constant expressions).

```cpp
constexpr int factorial(int n) {
    return (n <= 1) ? 1 : n * factorial(n - 1);
}

constexpr int fact5 = factorial(5); // Computed at compile time
```

### Evolution in C++14, C++17, C++20

- **C++14**: Fewer restrictions (loops, local variables allowed).
    
- **C++17**: `if constexpr` for compile-time branches.
    
- **C++20**: Even more features (e.g., try-catch in `constexpr`).
    

---

## noexcept Functions (C++11)

Promises not to throw exceptions.

```cpp
void safeFunction() noexcept {
    // ...
}
```

### Conditional noexcept

Depends on whether operations inside can throw:

```cpp
template<typename T>
void moveObject(T& dest, T& src) 
    noexcept(std::is_nothrow_move_constructible_v<T>) {
    dest = std::move(src);
}
```

### noexcept Operator

Checks if an expression is declared noexcept.

```cpp
if constexpr (noexcept(safeFunction())) {
    // ...
}
```

---

## nodiscard Attribute (C++17)

Warns if a function’s return value is ignored.

```cpp
[[nodiscard]] bool checkStatus() {
    return isOperational();
}

// C++20 message
[[nodiscard("Please handle the result!")]]
bool validateCredentials() {
    return performValidation();
}
```

---

## deprecated Attribute (C++14)

Marks a function as deprecated.

```cpp
[[deprecated]] void oldFunction() {
    // ...
}

[[deprecated("Use newFunction() instead")]]
void legacyFunction() {
    // ...
}
```

---

## Function Body and Scope Rules

A function body defines a new scope with its own lifetime rules.

```cpp
int globalVar = 10; // Global scope

void functionScope(int parameter) {
    int localVar = 20; // Local scope
    static int callCount = 0; // Persists across calls
    callCount++;
    
    if (localVar > 0) {
        int blockVar = 30; // Block scope
        // ...
    }
    // blockVar is inaccessible here
}
```

> **Note:** Don’t return references or pointers to local variables—those variables go out of scope.

---

## Best Practices

1. **Keep functions focused:** One clear purpose per function.
    
2. **Use meaningful names:** Make the function’s intent obvious.
    
3. **Choose parameter passing wisely:**
    
    - **By value:** Small or trivial types
        
    - **By const ref:** Large objects that aren’t modified
        
    - **By ref:** When modifications are required
        
4. **Return by value unless you have a specific need** for references or pointers.
    
5. **Use default arguments sparingly:** Keep them for truly optional parameters.
    
6. **Document parameters and return values:** Especially for public APIs.
    
7. **Consider `noexcept`:** Helps optimizers and documents intent.
    
8. **Use trailing return types** for complex or template-heavy return types.
    
9. **Consider `constexpr`** if compile-time evaluation is beneficial.
    
10. **Leverage `nodiscard`** when ignoring a return value is likely a bug.
    

---

**That’s it!** This file gives an overview of function declarations, definitions, and related language features in C++. By following these guidelines and best practices, you’ll write clearer, more maintainable code.