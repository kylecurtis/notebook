# Loops and Iteration in C++

Loops allow code to execute repeatedly until a condition is met (or forever). C++ provides a range of loop constructs, each well suited to specific iteration needs.

```cpp
#include <iostream> // For input/output
#include <vector> // For std::vector
#include <array> // For std::array
#include <algorithm> // For std::for_each, std::sort
#include <execution> // For parallel execution policies (C++17)
#include <numeric> // For std::accumulate
#include <string> // For std::string
```

---

## for Loop

### Traditional for Loop

The classical `for` loop has three parts: initialization, condition, and update:

```cpp
for (int i = 0; i < 10; ++i) {
    std::cout << i << " ";
}

int numbers[5] = {10, 20, 30, 40, 50};
for (int i = 0; i < 5; ++i) {
    std::cout << numbers[i] << " ";
}

// Countdown
for (int i = 10; i > 0; --i) {
    std::cout << i << " ";
}
```

### Comma Operator in for Loops

The comma operator `(,)` can separate multiple statements in initialization/update sections:

```cpp
for (int i = 0, j = 10; i < j; ++i, --j) {
    std::cout << "i: " << i << ", j: " << j << '\n';
}

// Multi-operation update
for (int i = 0; i < 10; ++i, std::cout << i << " ") {
    // empty body
}
```

### Multiple Counters in for Loops

Often used for 2D iteration or parallel arrays:

```cpp
int matrix[3][3] = {{1,2,3},{4,5,6},{7,8,9}};
for (int row = 0; row < 3; ++row) {
    for (int col = 0; col < 3; ++col) {
        std::cout << matrix[row][col] << " ";
    }
    std::cout << '\n';
}
```

### Omitting Loop Components

Any of the three `for` components can be omitted:

```cpp
// Omit initialization
int i = 0;
for (; i < 10; ++i) {
    // ...
}

// Omit condition (use break)
for (int i = 0;; ++i) {
    if (i >= 10) break;
    // ...
}

// Omit update (do it in the body)
for (int i = 0; i < 10; ) {
    std::cout << i << " ";
    ++i;
}

// Omit all => infinite loop
for (;;) {
    // ...
    break;
}
```

---

## while Loop

A `while` loop checks its condition before executing:

```cpp
int count = 0;
while (count < 5) {
    std::cout << count << " ";
    ++count;
}

std::string input;
while (input != "quit") {
    std::cout << "Enter command: ";
    std::cin >> input;
    // ...
}
```

### Pre-test vs Post-test Loops

- **Pre-test** (`while`): condition is checked _before_ entering the loop.
    
- **Post-test** (`do-while`): condition is checked _after_ executing the loop body at least once.
    

```cpp
// while
int x = 0;
while (x < 5) {
    std::cout << x << '\n';
    ++x;
}

// do-while
int y = 0;
do {
    std::cout << y << '\n';
    ++y;
} while (y < 5);
```

### Infinite Loops

A `while(true)` loop continues until a `break` or return:

```cpp
while (true) {
    int n;
    std::cin >> n;
    if (!std::cin) break; // or if(n==0) break;
}
```

---

## do-while Loop

Runs its body once before checking its condition:

```cpp
int i = 0;
do {
    std::cout << i << " ";
    ++i;
} while (i < 5);

int value;
do {
    std::cout << "Enter a positive number: ";
    std::cin >> value;
} while (value <= 0);
```

---

## Range-based for Loop (C++11)

A streamlined way to iterate over containers or arrays:

```cpp
int arr[] = {1, 2, 3};
for (int x : arr) {
    std::cout << x << " ";
}

std::vector<std::string> v = {"apple", "banana"};
for (const auto& fruit : v) {
    std::cout << fruit << " ";
}

// Modify elements
for (auto& elem : v) {
    elem += "!";
}
```

### Container Requirements

Range-based `for` uses `begin()` and `end()` (either as member or ADL-found free functions). Custom containers must provide them.

```cpp
class Custom {
    int data[5];
public:
    Custom() { for (int i = 0; i < 5; ++i) data[i] = i; }
    int* begin() { return &data[0]; }
    int* end() { return &data[5]; }
};

Custom c;
for (int val : c) {
    std::cout << val << " "; // 0 1 2 3 4
}
```

### Custom Range Support

You can define your own iterators to work with range-based `for`.

### Init-statement in Range-for (C++20)

C++20 allows an `init-statement` in a range-based for:

```cpp
for (auto v = std::vector{1,2,3}; const auto& x : v) {
    // ...
}
```

---

## break Statement

Exits a loop immediately:

```cpp
for (int i = 0; i < 100; ++i) {
    if (i * i > 100) {
        break;
    }
}

while (true) {
    std::string cmd;
    std::cin >> cmd;
    if (cmd == "exit") break;
}
```

### Breaking from Nested Loops

In C++, you must coordinate your breaks manually:

```cpp
bool done = false;
for (int i = 0; i < 10 && !done; ++i) {
    for (int j = 0; j < 10; ++j) {
        if (someCondition) {
            done = true;
            break;
        }
    }
}
```

### Labeled Breaks (Workarounds)

C++ doesn’t have official labeled breaks, but you can simulate them with flags, `goto`, or function returns.

---

## continue Statement

Skips the remaining loop body and continues with the next iteration:

```cpp
for (int i = 1; i <= 10; ++i) {
    if (i % 2 == 0) continue; // skip evens
    std::cout << i << " ";
}
```

---

## goto Statement and Labels

**Use sparingly**—`goto` can make logic harder to follow. Prefer structured alternatives.

```cpp
// Rare usage: break out of multiple loops
for (int i = 0; i < 10; ++i) {
    for (int j = 0; j < 10; ++j) {
        if (needToExit) {
            goto out;
        }
    }
}
out:
// continue code
```

### Appropriate Uses

- Low-level error handling in older C code
    
- Jumping to cleanup code (still rarely recommended in modern C++)
    

### Structured Programming Alternative

Use RAII and exceptions or dedicated cleanup objects, rather than `goto`.

---

## Infinite Loops with Control Flow

You can intentionally create loops that only exit via `break` or `return`:

```cpp
while (true) {
    // ...
    if (shouldStop()) break;
}

for (;;) {
    // infinite loop
}
```

---

## Loop Invariants

A **loop invariant** is a condition that holds true before and after each iteration:

```cpp
// Summation loop invariant: sum = sum of all elements up to i-1
int sum = 0;
for (int i = 0; i < arr.size(); ++i) {
    sum += arr[i];
}
```

---

## Loop Unrolling Techniques

Manual or compiler-based unrolling can speed up tight loops:

```cpp
// Manual unroll
int sum = 0;
int i = 0;
for (; i + 3 < size; i += 4) {
    sum += arr[i];
    sum += arr[i+1];
    sum += arr[i+2];
    sum += arr[i+3];
}
for (; i < size; ++i) {
    sum += arr[i];
}
```

---

## Duff's Device and Loop Optimization

A historical method of loop unrolling. Mostly for curiosity in modern C++.

```cpp
void sendBytes(const char* from, char* to, int count) {
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
```

---

## Iterator-based Loops vs Indexing

You can iterate containers by **index** or with **iterators**:

```cpp
std::vector<int> v = {1,2,3};

// Index-based
for (int i = 0; i < v.size(); ++i) {
    std::cout << v[i] << " ";
}

// Iterator-based
for (auto it = v.begin(); it != v.end(); ++it) {
    std::cout << *it << " ";
}

// Range-based for
for (auto x : v) {
    std::cout << x << " ";
}
```

---

## Parallel Algorithms and Execution Policies (C++17)

Allows you to run standard algorithms in parallel:

```cpp
std::vector<int> data(10000);
std::iota(data.begin(), data.end(), 0);

int sum = std::reduce(std::execution::par, data.begin(), data.end());

std::sort(std::execution::par, data.begin(), data.end());

std::for_each(std::execution::par, data.begin(), data.end(), [](int& x){ x *= x; });
```

---

## Best Practices

1. **Choose the right loop construct** for the job
    
2. **Keep loop logic simple**; break out complicated pieces
    
3. **Use break/continue** judiciously
    
4. **Leverage range-based for** whenever possible
    
5. **Use standard algorithms** (`std::for_each`, `std::transform`, etc.) instead of manual loops
    
6. **Consider RAII and structured programming** over `goto`
    
7. **Watch for infinite loop conditions** (use careful checks)
    
8. **Profile first** if performance is a concern, then consider unrolling, etc.