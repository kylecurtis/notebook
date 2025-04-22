# Control Flow in C++

This guide covers C++ control flow constructs including conditional logic, loops, and flow-altering keywords. These are foundational concepts that every professional C++ developer must understand.

---

## Conditional Statements

### `if`, `else if`, `else`

```cpp
int x{42};

if (x > 50) {
    // executes if x is greater than 50
} else if (x == 42) {
    // executes if x equals 42
} else {
    // executes otherwise
}
```

#### Initialization in if statements (C++17)

```cpp
if (int result = calculation(); result > 0) {
    // Use result
} else {
    // Result is also visible here
}
```

#### Constexpr if (C++17)

```cpp
template <typename T>
void process(T value) {
    if constexpr (std::is_integral_v<T>) {
        // Compile-time branch for integral types
    } else if constexpr (std::is_floating_point_v<T>) {
        // Compile-time branch for floating-point types
    } else {
        // Branch for other types
    }
}
```

#### Interview Question: if constexpr vs Regular if

**Q: What is the difference between `if constexpr` and a regular `if` statement?** 
**A:** `if constexpr` evaluates the condition at compile time and only compiles the branch that is taken. This means:

- Code in the non-taken branch is not instantiated (important for templates)
- The unused branch isn't checked for syntax errors in dependent contexts
- It enables templates to handle types that wouldn't compile in certain branches
- Regular `if` evaluates at runtime and both branches must be valid code

### Ternary Operator `?:`

```cpp
int max = (a > b) ? a : b;  // Returns a if a > b, otherwise b

// Can be chained, but use with caution for readability
int value = (x < 0) ? -1 : (x > 0) ? 1 : 0;  // Sign function
```

### `switch`

Use when comparing a value against several constants.

```cpp
int value{2};

switch (value) {
    case 1:
        // handle 1
        break;
    case 2:
        // handle 2
        break;
    case 3:  // Fallthrough - no break
    case 4:  // Both 3 and 4 execute this code
        // handle 3 and 4
        break;
    default:
        // fallback
        break;
}
```

#### Switch with initialization (C++17)

```cpp
switch (auto val = getValue(); val) {
    case 1: 
        // Use val here
        break;
    default:
        // val is also accessible here
        break;
}
```

#### Attributes for switch

```cpp
// C++17 [[fallthrough]] attribute
switch (value) {
    case 1:
        // Some operations
        [[fallthrough]]; // Explicitly indicates intentional fallthrough
    case 2:
        // Shared operations for both case 1 and 2
        break;
}
```

> Always include a `default` case to handle unexpected values.

#### Interview Question: switch Limitations

**Q: What are the limitations of the switch statement in C++?** **A:**

- Can only switch on integral types (including enum), characters, and (since C++17) `std::string_view`
- Case values must be compile-time constants (not variables)
- Cannot switch directly on floating-point values or strings (pre-C++17)
- Cannot switch on ranges of values (must use individual cases)
- All case statements share the same scope (variables defined in one case are visible in others)

---

## Looping Constructs

### `while` Loop

```cpp
int i{0};
while (i < 5) {
    ++i;
}
```

### `do-while` Loop

```cpp
int j{0};
do {
    ++j;
} while (j < 5);
```

> `do-while` guarantees the body runs at least once.

### `for` Loop

```cpp
for (int i{0}; i < 5; ++i) {
    // loop body
}
```

#### Flexible for loop initialization and update

```cpp
// Multiple initialization and increment expressions
for (int i = 0, j = 10; i < j; ++i, --j) {
    // i increases, j decreases until they meet
}

// Omitting sections (similar to while)
int k = 0;
for (; k < 10;) {
    ++k;
}

// Infinite loop
for (;;) {
    // Run until break statement
    if (condition) break;
}
```

### Range-Based `for` Loop (C++11+)

```cpp
#include <vector>

std::vector<int> numbers{1, 2, 3, 4, 5};
for (int num : numbers) {
    // access each element directly
}
```

Use `const` or references to avoid copies:

```cpp
for (const int& num : numbers) {
    // read-only access
}
```

#### Range-based for with initialization (C++20)

```cpp
for (auto data = getData(); auto& value : data) {
    // Use value
}
```

#### Interview Question: Range-based for Loop

**Q: What types can be used with range-based for loops, and what requirements must they meet?** **A:** A type can be used with range-based for loops if:

1. It provides `begin()` and `end()` member functions, OR
2. There are free functions `begin(container)` and `end(container)` in namespace scope
3. The iterators returned by begin/end are comparable and dereferenceable
4. C arrays also work automatically
5. For C++17 onward, the container can have different begin/end types (heterogeneous ranges)

---

## Flow Control Keywords

### `break`

Exits the nearest enclosing loop or `switch`.

```cpp
for (int i{0}; i < 10; ++i) {
    if (i == 5) break;
}
```

### `continue`

Skips the rest of the current iteration.

```cpp
for (int i{0}; i < 10; ++i) {
    if (i % 2 == 0) continue;  // skip even numbers
}
```

### `return`

Exits the current function, optionally returning a value.

```cpp
bool isPrime(int n) {
    if (n <= 1) return false;
    if (n <= 3) return true;
    
    if (n % 2 == 0 || n % 3 == 0) return false;
    
    for (int i = 5; i * i <= n; i += 6) {
        if (n % i == 0 || n % (i + 2) == 0)
            return false;
    }
    
    return true;
}
```

### `goto` (Avoid in modern C++)

```cpp
int x{0};
if (x == 0) goto skip;
// ...
skip:
// continue execution here
```

> `goto` is rarely used and discouraged due to readability and maintenance concerns.

#### Interview Question: goto Justification

**Q: Are there any legitimate use cases for `goto` in modern C++?** **A:** While generally discouraged, there are a few limited cases where `goto` might be justified:

1. Breaking out of deeply nested loops when `break` is insufficient
2. Error handling in resource acquisition sequences (though RAII is usually better)
3. Some state machine implementations
4. Performance-critical code where compiler optimizations benefit from goto
5. Low-level systems programming or embedded systems with specific patterns

However, in most modern C++ code, alternatives like exceptions, early returns, or refactoring into functions are preferred.

---

## Structured Binding (C++17)

Enables decomposing objects into multiple variables.

```cpp
#include <map>
#include <string>

std::map<std::string, int> scores{{"Alice", 95}, {"Bob", 87}};

// Iterate with structured binding
for (const auto& [name, score] : scores) {
    std::cout << name << ": " << score << std::endl;
}

// Array decomposition
int arr[] = {1, 2, 3};
auto [x, y, z] = arr;

// Tuple decomposition
std::tuple<int, double, std::string> tuple_data{42, 3.14, "hello"};
auto [i, d, s] = tuple_data;

// Custom type decomposition (requires get<> or destructuring capabilities)
struct Point { int x, y; };
Point p{10, 20};
auto [px, py] = p;  // Works if appropriate customization exists
```

#### Interview Question: Structured Binding

**Q: How does structured binding work with custom types?** **A:** For custom types to work with structured binding, one of the following must be true:

1. The type is an aggregate with public members (struct/class without constructors)
2. There are specializations of `std::tuple_size` and `std::tuple_element` for the type, and either:
    - A `get<N>()` function for the type in the same namespace, or
    - Member functions like `get<N>()` in the class
3. The class has non-static data members that are all public and direct

---

## Short-Circuit Evaluation

Logical operators `&&` and `||` evaluate left-to-right and stop early if possible.

```cpp
int x{0};
if (x != 0 && (10 / x > 1)) {
    // safe: right-hand expression is not evaluated if x == 0
}

// Check pointer before dereferencing
if (ptr != nullptr && ptr->value > 0) {
    // Safe: right-hand only evaluated if ptr is not null
}

// Set default when value not found
bool found = findValue(value) || (value = defaultValue, true);
```

#### Interview Question: Short-Circuit Evaluation

**Q: How can short-circuit evaluation be used to implement conditional assignment patterns?** **A:** Short-circuit evaluation enables patterns like:

```cpp
// The "Elvis operator": get value or default if null/invalid
result = value ? value : default_value;
// Using ||
result = value || default_value;  // Works when value is boolean or implicitly convertible

// Using && for conditional execution
x > 0 && executePositiveCase();  // Execute only if x > 0

// Using || for fallbacks
return firstAttempt() || secondAttempt() || fallback();  
// Try options in sequence until one succeeds (returns true)
```

These patterns can lead to more concise code but should be used judiciously for readability.

---

## Exceptions

Exception handling for error conditions:

```cpp
#include <stdexcept>

void processData(int value) {
    try {
        if (value < 0) {
            throw std::invalid_argument("Value cannot be negative");
        }
        
        // Process normally
        
    } catch (const std::invalid_argument& e) {
        // Handle specific exception
        std::cerr << "Invalid argument: " << e.what() << std::endl;
    } catch (const std::exception& e) {
        // Handle any standard exception
        std::cerr << "Exception: " << e.what() << std::endl;
    } catch (...) {
        // Catch any other exception
        std::cerr << "Unknown exception caught" << std::endl;
    }
}
```

#### Exception specifications (C++11/C++17)

```cpp
// C++11: Function may throw any exception
void func1();

// C++11: Function throws no exceptions (deprecated in C++17, removed in C++20)
void func2() throw();

// C++11 onwards: Function throws no exceptions (preferred)
void func3() noexcept;

// C++11 onwards: Function throws no exceptions if expression is true
void func4() noexcept(sizeof(int) > 4);
```

#### Interview Question: Exception Safety

**Q: What are the different levels of exception safety in C++?** **A:** C++ defines four levels of exception safety:

1. **No guarantee**: If an exception occurs, the program may be left in an invalid state
2. **Basic guarantee**: If an exception occurs, no resources are leaked and objects remain in a valid state (though not necessarily the original state)
3. **Strong guarantee**: If an exception occurs, the operation is rolled back (as if it never happened)
4. **No-throw guarantee**: The operation will not throw exceptions and will always succeed

Most C++ standard library components provide at least the basic guarantee, with many operations providing the strong guarantee where possible.

---

## Compiler Optimization and Control Flow

Control flow impacts compiler optimizations:

```cpp
// Likely/Unlikely attributes (C++20)
if (x > 0 [[likely]]) {
    // Compiler optimizes for this path
} else [[unlikely]] {
    // Less optimized path
}

// Manual loop unrolling for performance
for (int i = 0; i < 16; i += 4) {
    process(i);    // Manually unroll loop to reduce
    process(i+1);  // branch prediction overhead
    process(i+2);
    process(i+3);
}
```

#### Common optimization-friendly patterns

```cpp
// Hoisting invariant computations out of loops
int size = collection.size();  // Compute once
for (int i = 0; i < size; ++i) {
    // Use size
}

// Avoiding branch prediction misses
// Instead of:
for (int i = 0; i < size; ++i) {
    if (condition) { /* rare case */ }
    else { /* common case */ }
}

// Prefer:
for (int i = 0; i < size; ++i) {
    if (!condition) { /* common case */ }
    else { /* rare case */ }
}
```

#### Interview Question: Branch Prediction

**Q: How does branch prediction affect performance, and how can developers write branch-friendly code?** **A:** Branch prediction is a CPU optimization technique that tries to guess which way a conditional will go before knowing the actual value. Mispredictions cause pipeline stalls and hurt performance.

Developer strategies:

1. Make the most common case the first condition in if-else chains
2. Use `[[likely]]` and `[[unlikely]]` attributes (C++20)
3. Keep conditionals simple and predictable where possible
4. Consider branch-free alternatives for small operations (e.g., using math instead of conditionals)
5. Organize data structures to minimize branching in hot loops
6. Consider branchless programming techniques for performance-critical code

---

## Best Practices

- Always use `break` in `switch` cases unless fallthrough is intentional
    
- Use `[[fallthrough]]` attribute to indicate intentional switch fallthrough
    
- Prefer range-based `for` loops for cleaner and safer code
    
- Avoid `goto` unless absolutely necessary (e.g., low-level code, error handling in old codebases)
    
- Use short-circuit logic to guard expensive or unsafe operations
    
- Use `const` and references in range-based loops to avoid unnecessary copies
    
- Prefer compile-time decisions (`if constexpr`) over runtime conditionals when appropriate
    
- Keep error handling (exceptions) separate from normal control flow
    
- Structure your code to make the common case fast and branch-predictable
    
- Use structured bindings to make code working with tuples and structs more readable
    

---

## Common Technical Interview Questions

1. **Q:** What are the differences between `break`, `continue`, and `return`?  
    **A:** `break` exits only the innermost loop or switch, `continue` skips to the next iteration of the innermost loop, and `return` exits the entire function potentially with a return value.
    
2. **Q:** How would you break out of nested loops?  
    **A:** Options include:
    
    - Using a `goto` (rarely recommended)
    - Using a flag variable and checking it in each loop
    - Refactoring the nested loops into a function and using `return`
    - Using exceptions for exceptional cases
3. **Q:** How do you implement a loop that processes elements in groups of 4?  
    **A:**
    
    ```cpp
    for (size_t i = 0; i < size; i += 4) {
        // Process element i, i+1, i+2, i+3
        // Handle bounds checking if size isn't a multiple of 4
    }
    ```
    
4. **Q:** What is the difference between early returns and single-return programming styles?  
    **A:**
    
    - Early returns exit a function as soon as a condition is met, reducing nesting
    - Single-return style uses one return statement at the end of the function
    - Early returns can be clearer for validation and error conditions
    - Single-return can make resource cleanup more straightforward (though RAII in C++ often mitigates this concern)
5. **Q:** How can you make switch statements more type-safe in C++?  
    **A:**
    
    - Use `enum class` for switch values to ensure type safety
    - Add a default case that handles unexpected values, possibly with an assert
    - Consider compiler warnings like `-Wswitch` to warn about missing enum cases
    - In C++17+, use `if constexpr` as an alternative for type-based branching

---

## Summary

Control flow enables logic and repetition in programs. Mastering these constructs is critical for writing efficient and readable C++ code. Know how and when to use each type of loop or conditional for clarity and performance. Modern C++ (C++11 onward) has introduced many new control flow features that enable more expressive and safer programming patterns.