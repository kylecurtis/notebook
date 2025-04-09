# Function Declaration and Definition in C++

Functions are the fundamental building blocks of C++ programs, allowing code to be modular, reusable, and well-organized. This note covers the core aspects of function declaration and definition.

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <utility> // For std::move
```

## Function Syntax Elements

A typical function declaration has the following elements:

```cpp
// Return type, name, parameter list
return_type function_name(parameter_type1 parameter1, parameter_type2 parameter2...);

// Example
int calculateSum(int a, int b);

// With specifiers and qualifiers
inline constexpr int add(int a, int b) noexcept;
```

## Function Declarations vs Definitions

A function declaration specifies the function's interface without its implementation, while a definition includes the implementation.

```cpp
// Declaration (prototype) - typically in header files (.h or .hpp)
double calculateArea(double length, double width);

// Definition - typically in implementation files (.cpp)
double calculateArea(double length, double width) {
    return length * width;
}

// Combined declaration and definition
int square(int x) {
    return x * x;
}
```

Function declarations can appear multiple times in a program, but a non-inline function can only be defined once.

## Return Types

Functions return values to their caller, with several options for the return type.

### void Functions

Functions that don't return a value.

```cpp
// Function that performs an action without returning a value
void printMessage(const std::string& message) {
    std::cout << message << '\n';
}

// Early return is allowed
void processCommand(const std::string& cmd) {
    if (cmd.empty()) {
        return; // Exit function early
    }
    // Process command
}
```

### Value Return Types

Functions that return a value by copy.

```cpp
// Return by value
int multiplyByTwo(int value) {
    return value * 2;
}

// Returning a complex type
std::string createGreeting(const std::string& name) {
    return "Hello, " + name + "!";
}

// Return value optimization (RVO) - compiler optimization
std::vector<int> createSequence(int size) {
    std::vector<int> result;
    for (int i = 0; i < size; ++i) {
        result.push_back(i);
    }
    return result; // Copy is typically elided by the compiler
}
```

### Reference Return Types

Functions that return a reference to an existing object.

```cpp
// Return by reference - BE CAREFUL not to return references to local variables
int& getElement(std::vector<int>& vec, size_t index) {
    return vec[index]; // Returns reference to element in the vector
}

// Usage - can modify the returned reference
std::vector<int> numbers = {10, 20, 30};
getElement(numbers, 1) = 25; // Modifies the second element to 25

// DANGER - returning reference to local variable
// int& badFunction() {
//     int x = 10;
//     return x; // NEVER DO THIS - x is destroyed when function exits
// }
```

### Pointer Return Types

Functions that return a pointer to an object.

```cpp
// Return by pointer
int* findValue(std::vector<int>& vec, int value) {
    for (size_t i = 0; i < vec.size(); ++i) {
        if (vec[i] == value) {
            return &vec[i]; // Return pointer to found element
        }
    }
    return nullptr; // Not found
}

// Dynamic allocation (caller must delete)
int* createDynamicInt(int value) {
    return new int(value); // Allocates a new int
}
// Usage:
// int* dynamicValue = createDynamicInt(42);
// // Use dynamicValue
// delete dynamicValue; // Must deallocate memory
```

### auto Return Type (C++14)

Functions that deduce their return type.

```cpp
// Return type deduction with auto (C++14)
auto add(int a, int b) {
    return a + b; // Return type deduced as int
}

auto createPair(const std::string& key, int value) {
    return std::make_pair(key, value); // Returns std::pair<std::string, int>
}
```

## Parameter Passing Mechanisms

C++ offers several ways to pass arguments to functions.

### Pass by Value

The function receives a copy of the argument.

```cpp
// Pass by value - function gets a copy
void incrementCopy(int value) {
    value++; // Only affects the local copy
}

// Usage
int x = 10;
incrementCopy(x);
// x is still 10
```

### Pass by Reference

The function receives a reference to the original argument, allowing it to modify the original.

```cpp
// Pass by reference - function can modify the original
void increment(int& value) {
    value++; // Modifies the original variable
}

// Usage
int x = 10;
increment(x);
// x is now 11
```

### Pass by Constant Reference

The function receives a reference but cannot modify the original, combining efficiency with safety.

```cpp
// Pass by const reference - efficient but prevents modification
void printDetails(const std::string& text) {
    std::cout << "Length: " << text.length() << ", Content: " << text << '\n';
    // text += " modified"; // Error: cannot modify a const reference
}

// Usage
std::string name = "Example";
printDetails(name); // No copying of the string
```

### Pass by Pointer

The function receives a pointer to the original argument.

```cpp
// Pass by pointer - can be null or point to valid object
void modifyValue(int* ptr) {
    if (ptr) { // Check for null pointer
        (*ptr) *= 2; // Modify the value at the pointer's address
    }
}

// Usage
int x = 10;
modifyValue(&x);
// x is now 20

modifyValue(nullptr); // Safe - function checks for null
```

### Pass by Rvalue Reference

Used for move semantics, allowing efficient transfer of resources.

```cpp
// Pass by rvalue reference - for move semantics
void processVector(std::vector<int>&& vec) {
    // Function takes ownership of the vector's resources
    vec.push_back(100);
    // Process vec
}

// Usage
processVector(std::vector<int>{1, 2, 3}); // Temporary object

// Move an existing object
std::vector<int> numbers = {5, 10, 15};
processVector(std::move(numbers)); // numbers is now in a valid but unspecified state
```

## Parameter Lists

Functions can take various types of parameter lists.

### Empty Parameter Lists

Functions that take no arguments.

```cpp
// Empty parameter list
int getCurrentTime() {
    // Return current timestamp
    return static_cast<int>(time(nullptr));
}

// C++11 style empty parameter list
void doNothing() {
    // Function takes no parameters and does nothing
}

// Pre-C++11 style (explicit void)
void doAlsoNothing(void) {
    // Function takes no parameters and does nothing
}
```

### void Parameter

In C++, a parameter list with `void` means the function takes no parameters.

```cpp
// void parameter (same as empty parameter list)
double getPi(void) {
    return 3.14159265359;
}
```

### Default Arguments

Specify default values for parameters, which are used when arguments are omitted.

```cpp
// Default arguments
void setConfiguration(bool logging = false, int cacheSize = 1024, const std::string& mode = "normal") {
    // Function implementation
}

// Usage
setConfiguration(); // All defaults
setConfiguration(true); // Only first argument provided
setConfiguration(true, 2048); // First two arguments provided
setConfiguration(true, 2048, "enhanced"); // All arguments provided

// Default arguments must be at the end of the parameter list
// void badFunction(int a = 1, int b); // Error: default followed by non-default

// Default arguments typically go in the declaration, not the definition
void showMessage(const std::string& message, bool showTimestamp = true);

void showMessage(const std::string& message, bool showTimestamp) {
    // Implementation
}
```

### Variadic Functions (C-style)

Functions that accept a variable number of arguments (old C style).

```cpp
#include <cstdarg>

// C-style variadic function
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

// Usage
int result = sum(4, 10, 20, 30, 40); // Sums 4 values
```

### Function Parameter Pack (C++11)

Modern C++ variadic templates for type-safe variable arguments.

```cpp
// Variadic template function (C++11)
template<typename... Args>
void printAll(Args... args) {
    // Base case - fold expression (C++17)
    ((std::cout << args << ' '), ...);
    std::cout << '\n';
}

// Pre-C++17 recursive variadic template
template<typename T>
void print(T t) {
    std::cout << t << '\n';
}

template<typename T, typename... Args>
void print(T t, Args... args) {
    std::cout << t << ' ';
    print(args...);
}

// Usage
printAll(1, "Hello", 3.14, 'a');
print(1, "Hello", 3.14, 'a');
```

## Function Signatures

A function's signature consists of its name and parameter types. Return type is not part of the signature.

```cpp
// These functions have different signatures
void process(int value);
void process(double value);
void process(const std::string& value);

// These functions have the same signature (error)
// double calculate(int a, int b);
// int calculate(int a, int b); // Error: redefinition
```

## Trailing Return Type Syntax (C++11)

Alternative syntax for specifying return types, especially useful with templates.

```cpp
// Traditional syntax
int multiply(int a, int b);

// Trailing return type syntax
auto multiply(int a, int b) -> int;

// Particularly useful for complex return types
auto getNameValuePair() -> std::pair<std::string, int> {
    return {"example", 42};
}

// Useful for templates where return type depends on arguments
template<typename T, typename U>
auto add(T a, U b) -> decltype(a + b) {
    return a + b;
}
```

## Linkage Specifications

Control how functions interact with code compiled by other compilers or in other languages.

### extern "C"

Specifies C linkage for compatibility with C code.

```cpp
// C linkage for a single function
extern "C" void cStyleFunction(int arg);

// C linkage for multiple functions
extern "C" {
    double calculateValue(double input);
    int processData(const char* data, size_t length);
}

// Typical usage in header files for cross-language compatibility
#ifdef __cplusplus
extern "C" {
#endif

// Function declarations here

#ifdef __cplusplus
} // end of extern "C" block
#endif
```

### Language Linkage and ABI

Affects the Application Binary Interface (ABI) used for the function.

```cpp
// C++ linkage (default)
void cppFunction() {
    // Uses C++ name mangling
}

// C linkage (no name mangling)
extern "C" void cFunction() {
    // Uses C calling convention
}

// For using functions from a specific DLL in Windows
extern "Windows" void windowsSpecificFunction();

// Other language examples (implementation-defined)
// extern "Fortran" void fortranFunction();
// extern "Pascal" void pascalFunction();
```

## Inline Functions

Suggest to the compiler that the function should be expanded at the call site.

### inline Keyword

```cpp
// inline function declaration
inline int min(int a, int b) {
    return (a < b) ? a : b;
}

// Class member functions defined within the class are implicitly inline
class Example {
public:
    void method() { // Implicitly inline
        // Implementation
    }
};
```

### Compiler Inlining Decisions

The `inline` keyword is just a suggestion; the compiler makes the final decision.

```cpp
// Compiler may choose to inline this even without the keyword
int square(int x) {
    return x * x;
}

// Compiler may choose not to inline this despite the keyword
inline int complexFunction(int x) {
    int result = 0;
    for (int i = 0; i < x; ++i) {
        result += i * i;
        if (i % 2 == 0) {
            result -= i;
        }
    }
    return result;
}
```

### Link-time Optimization

Modern compilers can make inlining decisions across translation units.

```cpp
// In header file
inline int optimizedFunction(int x) {
    return x * x + x + 1;
}

// Usage in different .cpp files still allows inlining with LTO enabled
// The linker can see the function body and decide to inline across files
```

## constexpr Functions (C++11)

Functions that can be evaluated at compile time.

### Rules and Restrictions

```cpp
// Basic constexpr function
constexpr int factorial(int n) {
    return (n <= 1) ? 1 : n * factorial(n - 1);
}

// Usage at compile time
constexpr int fact5 = factorial(5); // Evaluated at compile time

// constexpr functions can also be used at runtime
int runtime_value = 4;
int fact_runtime = factorial(runtime_value); // Evaluated at runtime
```

### Evolution in C++14, C++17, C++20

```cpp
// C++11: Strict restrictions (only return statements)
constexpr int square_cpp11(int x) {
    return x * x;
}

// C++14: Allows more statements, variables, loops
constexpr int factorial_cpp14(int n) {
    int result = 1;
    for (int i = 2; i <= n; ++i) {
        result *= i;
    }
    return result;
}

// C++17: Allows if constexpr for compile-time conditionals
template<typename T>
constexpr auto get_value(T t) {
    if constexpr (std::is_pointer_v<T>) {
        return *t; // Only instantiated when T is a pointer
    } else {
        return t; // Only instantiated when T is not a pointer
    }
}

// C++20: Allows try-catch, virtual (not shown due to complexity)
```

## noexcept Functions (C++11)

Specifies that a function does not throw exceptions or propagate exceptions.

```cpp
// Simple noexcept function
void safeFunction() noexcept {
    // This function promises not to throw exceptions
}

// Function that might throw
void unsafeFunction() {
    throw std::runtime_error("Error occurred");
}
```

### Conditional noexcept

```cpp
// Conditional noexcept - depends on whether operations inside might throw
template<typename T>
void processValue(T value) noexcept(noexcept(T{})) {
    T temp{};
    // Process value
}

// noexcept based on whether std::is_nothrow_move_constructible
template<typename T>
void moveObject(T& dest, T& src) noexcept(std::is_nothrow_move_constructible_v<T>) {
    dest = std::move(src);
}
```

### noexcept Operator

Tests whether an expression is declared to not throw exceptions.

```cpp
// Using noexcept operator
void example() {
    // Check if functions are noexcept
    constexpr bool safe = noexcept(safeFunction());    // true
    constexpr bool unsafe = noexcept(unsafeFunction()); // false
    
    // Use in conditional compilation
    if constexpr (noexcept(safeFunction())) {
        // Do something optimized for non-throwing functions
    }
}
```

## nodiscard Attribute (C++17)

Warns if the return value of a function is ignored.

```cpp
// [[nodiscard]] attribute
[[nodiscard]] bool checkStatus() {
    return isOperational();
}

// Usage - compiler warning if result ignored
// checkStatus(); // Warning: discarded return value

// With message (C++20)
[[nodiscard("Critical security check should not be ignored")]]
bool validateCredentials() {
    return performValidation();
}
```

## deprecated Attribute (C++14)

Indicates that a function is deprecated and may be removed in future versions.

```cpp
// [[deprecated]] attribute
[[deprecated]] void oldFunction() {
    // Implementation
}

// With custom message
[[deprecated("Use newFunction() instead")]]
void legacyFunction() {
    // Implementation
}

// Usage generates compiler warning
// legacyFunction(); // Warning: 'legacyFunction' is deprecated
```

## Function Body and Scope Rules

The function body defines a new scope with its own lifetime rules.

```cpp
// Scope demonstration
int globalVar = 10; // Global scope

void functionScope(int parameter) {
    // parameter is in function scope
    
    int localVar = 20; // Local scope
    
    if (localVar > 0) {
        int blockVar = 30; // Block scope
        // Can access globalVar, parameter, localVar, and blockVar here
    }
    
    // blockVar not accessible here
    
    // Static local variables persist between function calls
    static int callCount = 0;
    callCount++;
    std::cout << "Function called " << callCount << " times\n";
    
    // Local variables are destroyed when function exits
} // localVar, parameter are destroyed here

// Shadow variables
void shadowExample(int x) {
    int x = 20; // Error: redeclaration of parameter 'x'
    
    {
        int y = 10;
        {
            // This y shadows the outer y
            int y = 20;
            std::cout << y << '\n'; // Prints 20
        }
        std::cout << y << '\n'; // Prints 10
    }
}
```

## Best Practices

1. **Keep functions focused:** Each function should have a single purpose.
    
2. **Use meaningful names:** Function names should clearly indicate what the function does.
    
3. **Choose appropriate parameter passing:**
    
    - Use pass by value for small objects
    - Use pass by const reference for larger objects that don't need modification
    - Use pass by reference for objects that need to be modified
4. **Return by value for most cases:**
    
    - Modern compilers optimize away unnecessary copies
    - Return by reference only when returning a reference to an existing object
5. **Use default arguments sparingly:**
    
    - Only use defaults for truly optional parameters
    - Don't change default values in updates (breaks existing code)
6. **Document parameters and return values:**
    
    - Especially important for public APIs
    - Consider using noexcept for functions that won't throw
7. **Use trailing return types for complex cases:**
    
    - Particularly useful with templates
    - Improves readability with complex return types
8. **Consider constexpr for compile-time computation:**
    
    - Improves performance for values known at compile time
    - Makes intent clear to both compiler and other developers
9. **Declare functions inline in header files:**
    
    - Necessary for template functions
    - Helps compiler optimize across translation units
10. **Use nodiscard for functions whose return values should not be ignored:**
    
    - Particularly important for error codes and boolean returns