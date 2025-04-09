# Loops and Iteration in C++

Loops allow programs to execute a block of code repeatedly. C++ provides several loop constructs to handle different iteration needs efficiently.

```cpp
#include <iostream>   // For input/output operations
#include <vector>     // For vector container
#include <array>      // For array container
#include <algorithm>  // For standard algorithms
#include <execution>  // For parallel execution policies (C++17)
#include <string>     // For string operations
#include <numeric>    // For numeric operations
```

## for Loop

The most versatile loop construct, typically used when the number of iterations is known.

### Traditional for Loop

Consists of initialization, condition, and update statements.

```cpp
// Basic for loop
for (int i = 0; i < 10; ++i) {
    std::cout << i << " ";
}

// Iterating over an array
int numbers[5] = {10, 20, 30, 40, 50};
for (int i = 0; i < 5; ++i) {
    std::cout << numbers[i] << " ";
}

// Countdown loop
for (int i = 10; i > 0; --i) {
    std::cout << i << " ";
}

// Step size other than 1
for (int i = 0; i <= 10; i += 2) {
    std::cout << i << " "; // Prints even numbers 0-10
}
```

### Comma Operator in for Loops

The comma operator allows multiple expressions where one is expected.

```cpp
// Multiple variables initialized and updated
for (int i = 0, j = 10; i < j; ++i, --j) {
    std::cout << "i: " << i << ", j: " << j << '\n';
}

// Initializing multiple counters with different types
for (int i = 0, double x = 0.0; i < 5; ++i, x += 0.5) {
    std::cout << "i: " << i << ", x: " << x << '\n';
}

// Multiple operations in update section
for (int i = 0; i < 10; ++i, std::cout << i << " ") {
    // Loop body can be empty
}
```

### Multiple Counters in for Loops

Useful for nested data structures or coordinated counting.

```cpp
// Traversing a 2D array by rows and columns
int matrix[3][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};

for (int row = 0; row < 3; ++row) {
    for (int col = 0; col < 3; ++col) {
        std::cout << matrix[row][col] << " ";
    }
    std::cout << '\n';
}

// Processing pairs of elements from two arrays
int array1[5] = {1, 2, 3, 4, 5};
int array2[5] = {10, 20, 30, 40, 50};

for (int i = 0, j = 4; i < 5; ++i, --j) {
    std::cout << array1[i] << " + " << array2[j] << " = " 
              << (array1[i] + array2[j]) << '\n';
}
```

### Omitting Loop Components

Any part of the for loop can be omitted for specialized control flow.

```cpp
// Initialization outside the loop
int i = 0;
for (; i < 10; ++i) {
    std::cout << i << " ";
}

// Condition checked inside the loop
for (int i = 0;; ++i) {
    if (i >= 10) break;
    std::cout << i << " ";
}

// Update performed inside the loop
for (int i = 0; i < 10;) {
    std::cout << i << " ";
    ++i;
}

// All components omitted (infinite loop)
for (;;) {
    static int i = 0;
    if (i >= 10) break;
    std::cout << i++ << " ";
}
```

## while Loop

Executes a block of code as long as the condition is true.

```cpp
// Basic while loop
int count = 0;
while (count < 5) {
    std::cout << count << " ";
    ++count;
}

// Processing user input
std::string input;
while (input != "quit") {
    std::cout << "Enter command (or 'quit' to exit): ";
    std::cin >> input;
    // Process input...
}

// Processing with condition calculated inside loop
int num = 1024;
while (num > 0) {
    std::cout << (num & 1); // Print binary representation
    num >>= 1;
}
```

### Pre-test vs Post-test Loops

`while` is a pre-test loop, checking the condition before execution.

```cpp
// Pre-test (while) - may execute zero times
int x = 10;
while (x < 10) { // Condition is false immediately
    std::cout << "This won't execute";
    ++x;
}

// Post-test (do-while) - always executes at least once
int y = 10;
do {
    std::cout << "This executes once";
    ++y;
} while (y < 10);
```

### Infinite Loops

Can be created when the condition never becomes false.

```cpp
// Deliberate infinite loop with break condition
while (true) {
    std::cout << "Enter a number (0 to quit): ";
    int n;
    std::cin >> n;
    if (n == 0) break;
    std::cout << "You entered: " << n << '\n';
}

// Potential accidental infinite loop
int j = 10;
while (j >= 0) {
    std::cout << j << " ";
    j++; // Oops, incrementing instead of decrementing
    // Should be j-- to terminate
}

// Loop with exit condition inside
while (true) {
    static int counter = 0;
    if (++counter > 10) break;
    std::cout << counter << " ";
}
```

## do-while Loop

Executes the loop body at least once, then checks the condition.

```cpp
// Basic do-while loop
int i = 0;
do {
    std::cout << i << " ";
    ++i;
} while (i < 5);

// Input validation loop
int value;
do {
    std::cout << "Enter a positive number: ";
    std::cin >> value;
} while (value <= 0);

// Menu system
int choice;
do {
    std::cout << "Menu:\n";
    std::cout << "1. Option One\n";
    std::cout << "2. Option Two\n";
    std::cout << "3. Exit\n";
    std::cout << "Enter choice: ";
    std::cin >> choice;
    
    switch (choice) {
        case 1: std::cout << "Selected Option One\n"; break;
        case 2: std::cout << "Selected Option Two\n"; break;
        case 3: std::cout << "Exiting...\n"; break;
        default: std::cout << "Invalid choice\n";
    }
} while (choice != 3);
```

## Range-based for Loop (C++11)

Simplifies iteration over containers and arrays.

```cpp
// Iterating over array
int numbers[] = {1, 2, 3, 4, 5};
for (int num : numbers) {
    std::cout << num << " ";
}

// Iterating over vector
std::vector<std::string> fruits = {"apple", "banana", "cherry"};
for (const std::string& fruit : fruits) {
    std::cout << fruit << " ";
}

// Using auto for type deduction
std::vector<std::pair<std::string, int>> items = {{"apple", 5}, {"banana", 8}};
for (const auto& item : items) {
    std::cout << item.first << ": " << item.second << '\n';
}

// Modifying elements with reference
std::vector<int> scores = {70, 85, 90, 65};
for (auto& score : scores) {
    score += 5; // Add bonus points
}
```

### Container Requirements

For a type to work with range-based for, it must:

```cpp
// A type works with range-based for if:
// 1. It has begin() and end() member functions, OR
// 2. begin(container) and end(container) free functions are defined

// Custom container example
class NumberSequence {
private:
    int* data;
    size_t size;
    
public:
    // Iterator class for our container
    class Iterator {
    private:
        int* ptr;
    public:
        Iterator(int* p) : ptr(p) {}
        bool operator!=(const Iterator& other) const { return ptr != other.ptr; }
        Iterator& operator++() { ++ptr; return *this; }
        int& operator*() const { return *ptr; }
    };
    
    NumberSequence(size_t n) : size(n) {
        data = new int[size];
        for (size_t i = 0; i < size; ++i) {
            data[i] = i * 10;
        }
    }
    
    Iterator begin() { return Iterator(data); }
    Iterator end() { return Iterator(data + size); }
    
    ~NumberSequence() { delete[] data; }
};

// Usage
NumberSequence seq(5);
for (int value : seq) {
    std::cout << value << " "; // Outputs: 0 10 20 30 40
}
```

### Custom Range Support

Building types that work with range-based for loops.

```cpp
// Simple range type
class Range {
private:
    int start;
    int end;
    
public:
    Range(int start, int end) : start(start), end(end) {}
    
    class Iterator {
    private:
        int value;
    public:
        Iterator(int value) : value(value) {}
        bool operator!=(const Iterator& other) const { return value != other.value; }
        int operator*() const { return value; }
        Iterator& operator++() { ++value; return *this; }
    };
    
    Iterator begin() const { return Iterator(start); }
    Iterator end() const { return Iterator(end); }
};

// Usage
for (int i : Range(1, 5)) {
    std::cout << i << " "; // Outputs: 1 2 3 4
}
```

### Init-statement in Range-for (C++20)

Allows initializing variables in the loop header.

```cpp
// C++20 feature: init-statement in range-based for
// Compiler-dependent
for (auto vec = std::vector{1, 2, 3, 4, 5}; const auto& val : vec) {
    std::cout << val << " ";
}

// Creating a container in the loop init
for (auto data = getData(); const auto& element : data) {
    // Process element
}

// With custom range
for (auto range = Range(1, 5); int i : range) {
    std::cout << i << " ";
}
```

## break Statement

Exits the loop immediately, skipping remaining iterations.

```cpp
// Breaking from a for loop
for (int i = 0; i < 100; ++i) {
    if (i * i > 100) {
        std::cout << "First square greater than 100: " << i * i << '\n';
        break;
    }
}

// Breaking when finding an element
int numbers[] = {3, 7, 2, 5, 8, 1};
int target = 5;
bool found = false;

for (int num : numbers) {
    if (num == target) {
        found = true;
        break;
    }
}

// Early exit from while loop
std::string input;
while (true) {
    std::cout << "Enter text (type 'exit' to quit): ";
    std::getline(std::cin, input);
    if (input == "exit") {
        break;
    }
    // Process input
}
```

### Breaking from Nested Loops

```cpp
// Using a flag to break from nested loops
bool found = false;
for (int i = 0; i < 10 && !found; ++i) {
    for (int j = 0; j < 10; ++j) {
        if (matrix[i][j] == target) {
            std::cout << "Found at (" << i << ", " << j << ")\n";
            found = true;
            break;
        }
    }
}

// Using a function to break from deep nesting
auto findInMatrix = [&matrix, target]() -> std::pair<int, int> {
    for (int i = 0; i < 10; ++i) {
        for (int j = 0; j < 10; ++j) {
            if (matrix[i][j] == target) {
                return {i, j};
            }
        }
    }
    return {-1, -1}; // Not found
};

auto [row, col] = findInMatrix();
```

### Labeled Breaks (Workarounds)

C++ doesn't have labeled breaks, but there are workarounds.

```cpp
// Using goto as a labeled break (use cautiously)
for (int i = 0; i < 10; ++i) {
    for (int j = 0; j < 10; ++j) {
        if (matrix[i][j] == target) {
            std::cout << "Found at (" << i << ", " << j << ")\n";
            goto found;
        }
    }
}
found:
// Continue execution after the nested loops

// Using do...while(false) for early exit
do {
    for (int i = 0; i < 10; ++i) {
        for (int j = 0; j < 10; ++j) {
            if (matrix[i][j] == target) {
                std::cout << "Found at (" << i << ", " << j << ")\n";
                break; // Breaks inner loop
            }
        }
        // Check if we need to break from the outer loop
        if (found) break;
    }
} while (false); // Execute exactly once
```

## continue Statement

Skips the current iteration and proceeds to the next.

```cpp
// Skipping even numbers
for (int i = 1; i <= 10; ++i) {
    if (i % 2 == 0) {
        continue; // Skip even numbers
    }
    std::cout << i << " "; // Print only odd numbers
}

// Skipping invalid values in processing
std::vector<int> values = {-2, 5, 0, -3, 7, 9, 0};
for (int val : values) {
    if (val <= 0) {
        continue; // Skip non-positive values
    }
    std::cout << "Processing " << val << '\n';
}

// Handling specific cases separately
while (true) {
    Command cmd = getNextCommand();
    if (cmd.isSpecial()) {
        handleSpecialCommand(cmd);
        continue;
    }
    // Regular command processing
}
```

## goto Statement and Labels

Jumps to a labeled statement (use sparingly).

```cpp
// Error handling with goto
int result = 0;
FILE* file = fopen("data.txt", "r");
if (!file) {
    goto cleanup;
}

// Process file
result = processFile(file);
if (result < 0) {
    goto cleanup;
}

// More processing
result = finalizeProcessing();

cleanup:
if (file) {
    fclose(file);
}
return result;
```

### Appropriate Uses

```cpp
// Cleanup in error handling
int complexOperation() {
    Resource* r1 = allocateResource1();
    if (!r1) {
        return -1;
    }
    
    Resource* r2 = allocateResource2();
    if (!r2) {
        releaseResource1(r1);
        return -1;
    }
    
    if (operationFailed()) {
        releaseResource2(r2);
        releaseResource1(r1);
        return -1;
    }
    
    // Success path
    releaseResource2(r2);
    releaseResource1(r1);
    return 0;
}

// With goto (in C-style code)
int complexOperationWithGoto() {
    Resource* r1 = nullptr;
    Resource* r2 = nullptr;
    
    r1 = allocateResource1();
    if (!r1) {
        goto fail;
    }
    
    r2 = allocateResource2();
    if (!r2) {
        goto fail;
    }
    
    if (operationFailed()) {
        goto fail;
    }
    
    // Success path
    releaseResource2(r2);
    releaseResource1(r1);
    return 0;
    
fail:
    if (r2) releaseResource2(r2);
    if (r1) releaseResource1(r1);
    return -1;
}
```

### Structured Programming Alternative

Modern C++ provides better alternatives to `goto`.

```cpp
// Using RAII instead of goto
class ResourceGuard {
private:
    Resource* res;
public:
    ResourceGuard(Resource* r) : res(r) {}
    ~ResourceGuard() { if (res) releaseResource(res); }
};

int safeComplexOperation() {
    auto r1 = allocateResource1();
    if (!r1) return -1;
    ResourceGuard guard1(r1);
    
    auto r2 = allocateResource2();
    if (!r2) return -1;
    ResourceGuard guard2(r2);
    
    if (operationFailed()) {
        return -1;
    }
    
    // Resources automatically cleaned up by guards
    return 0;
}
```

## Infinite Loops with Control Flow

Loops that run indefinitely until explicitly broken.

```cpp
// Infinite loop with break
while (true) {
    std::cout << "Enter command: ";
    std::string cmd;
    std::getline(std::cin, cmd);
    
    if (cmd == "quit") {
        break;
    }
    
    processCommand(cmd);
}

// Event loop pattern
for (;;) {
    Event event = getNextEvent();
    if (event.type == Event::QUIT) {
        break;
    }
    handleEvent(event);
}

// Game loop example
bool running = true;
while (running) {
    processInput();
    updateGameState();
    render();
    
    if (shouldExit()) {
        running = false;
    }
}
```

## Loop Invariants

Conditions that remain true throughout a loop's execution.

```cpp
// Loop with invariant: sum contains the sum of values[0] through values[i-1]
int calculateSum(const std::vector<int>& values) {
    int sum = 0; // Initially sum of values[0..0-1] which is empty (sum = 0)
    
    for (int i = 0; i < values.size(); ++i) {
        // At this point, sum = values[0] + values[1] + ... + values[i-1]
        sum += values[i];
        // Now, sum = values[0] + values[1] + ... + values[i]
    }
    
    // At loop exit, sum = values[0] + values[1] + ... + values[n-1]
    return sum;
}

// Binary search with loop invariant:
// If target exists, it's in the range [left, right]
int binarySearch(const std::vector<int>& sorted, int target) {
    int left = 0;
    int right = sorted.size() - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (sorted[mid] == target) {
            return mid; // Found
        }
        if (sorted[mid] < target) {
            left = mid + 1; // Target must be in right half
        } else {
            right = mid - 1; // Target must be in left half
        }
    }
    
    return -1; // Not found
}
```

## Loop Unrolling Techniques

Reducing loop iterations to improve performance.

```cpp
// Regular loop
int sum = 0;
for (int i = 0; i < 1000; ++i) {
    sum += data[i];
}

// Manually unrolled loop (4x)
int sum = 0;
int i = 0;
for (; i < 996; i += 4) {
    sum += data[i];
    sum += data[i + 1];
    sum += data[i + 2];
    sum += data[i + 3];
}
// Handle remaining elements
for (; i < 1000; ++i) {
    sum += data[i];
}

// Unrolled with std::accumulate
// The compiler might automatically unroll this
int sum = std::accumulate(data, data + 1000, 0);

// Unrolled with loop tiling (blocking) for better cache usage
const int BLOCK_SIZE = 64; // Adjust based on cache size
int sum = 0;
for (int i = 0; i < 1000; i += BLOCK_SIZE) {
    int end = std::min(i + BLOCK_SIZE, 1000);
    for (int j = i; j < end; ++j) {
        sum += data[j];
    }
}
```

## Duff's Device and Loop Optimization

```cpp
// Duff's device: unrolled loop with jump into the middle
// Note: This is mostly a historical curiosity in C++
void sendBytes(char* to, const char* from, int count) {
    int n = (count + 7) / 8;
    switch (count % 8) {
    case 0: do { *to++ = *from++;
    case 7:      *to++ = *from++;
    case 6:      *to++ = *from++;
    case 5:      *to++ = *from++;
    case 4:      *to++ = *from++;
    case 3:      *to++ = *from++;
    case 2:      *to++ = *from++;
    case 1:      *to++ = *from++;
            } while (--n > 0);
    }
}

// Modern equivalent using template metaprogramming
template<int N>
struct Unroller {
    static void unroll(int* dest, const int* src) {
        Unroller<N-1>::unroll(dest, src);
        dest[N-1] = src[N-1];
    }
};

template<>
struct Unroller<0> {
    static void unroll(int* dest, const int* src) {}
};

// Usage
int source[8] = {1, 2, 3, 4, 5, 6, 7, 8};
int destination[8] = {0};
Unroller<8>::unroll(destination, source);
```

## Iterator-based Loops vs Indexing

```cpp
// Index-based iteration
std::vector<int> vec = {1, 2, 3, 4, 5};
for (size_t i = 0; i < vec.size(); ++i) {
    std::cout << vec[i] << " ";
}

// Iterator-based iteration
for (auto it = vec.begin(); it != vec.end(); ++it) {
    std::cout << *it << " ";
}

// Modern range-based for (best for most cases)
for (const auto& element : vec) {
    std::cout << element << " ";
}

// Reverse iteration with indices
for (int i = vec.size() - 1; i >= 0; --i) {
    std::cout << vec[i] << " ";
}

// Reverse iteration with iterators
for (auto it = vec.rbegin(); it != vec.rend(); ++it) {
    std::cout << *it << " ";
}

// Using iterators with standard algorithms
std::for_each(vec.begin(), vec.end(), [](int n) {
    std::cout << n << " ";
});
```

## Parallel Algorithms and Execution Policies (C++17)

Execution policies allow standard algorithms to run in parallel.

```cpp
#include <execution>

// Sequential execution
std::vector<int> vec(10000);
std::iota(vec.begin(), vec.end(), 0); // Fill with 0, 1, 2, ...

// Find sum using different execution policies
auto sum1 = std::reduce(vec.begin(), vec.end()); // Sequential

// Parallel execution
auto sum2 = std::reduce(
    std::execution::par,
    vec.begin(), vec.end()
);

// Parallel vectorized execution
auto sum3 = std::reduce(
    std::execution::par_unseq,
    vec.begin(), vec.end()
);

// Sorting with parallel execution
std::sort(
    std::execution::par,
    vec.begin(), vec.end()
);

// For-each with parallel execution
std::for_each(
    std::execution::par,
    vec.begin(), vec.end(),
    [](int& x) { x = x * x; }
);
```

## Best Practices

1. **Choose the appropriate loop construct:**
    
    - Use `for` when the number of iterations is known
    - Use `while` when the termination condition is checked at the beginning
    - Use `do-while` when the loop must execute at least once
    - Use range-based `for` when iterating over collections
2. **Optimize loop bodies:**
    
    - Move invariant calculations outside the loop
    - Minimize work inside the innermost loops
    - Consider loop unrolling for performance-critical code
3. **Use break and continue appropriately:**
    
    - Use `break` to exit a loop early when a condition is met
    - Use `continue` to skip the remainder of a loop body
    - Avoid complex control flow that makes loops hard to understand
4. **Minimize variable scope:**
    
    - Declare loop variables in the for-loop initializer when possible
    - Use C++17's init-statement in if/switch within loops
5. **Consider iterator-based loops over index-based loops:**
    
    - More idiomatic C++ style
    - Safer with STL containers
    - Less prone to off-by-one errors
6. **Avoid `goto` when possible:**
    
    - Prefer structured constructs like functions, loops and conditionals
    - Use exception handling for error paths
    - Consider RAII for resource management
7. **Use standard algorithms instead of manual loops when appropriate:**
    
    - More expressive and maintainable
    - Often more optimized than hand-written loops
    - Easier to parallelize with execution policies