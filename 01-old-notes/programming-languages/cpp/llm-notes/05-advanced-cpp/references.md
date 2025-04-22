# References in C++

C++ **references** provide an alternate way to access or modify objects without the explicit pointer syntax. They come in multiple varieties—lvalue references, rvalue references, forwarding references—each with different roles. This note covers references in depth.

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <functional> // For std::reference_wrapper
``` 

---

## Lvalue References

Lvalue references (type `T&`) bind to **lvalue objects**, meaning objects that have a persistent address in memory. They act like aliases for an existing object, with no explicit pointer syntax.

### Reference Variables

```cpp
int x = 10;
int& ref = x; // ref is an alias for x

ref = 20;     // modifies x
std::cout << x << "\n"; // 20
```

- Must be initialized to an existing object (cannot be null or uninitialized).
    
- Cannot be reassigned after initialization.
    

### Reference Parameters

Pass arguments by reference to avoid copying or to allow modifications:

```cpp
void increment(int& r) {
    ++r; // modifies the original argument
}

int a = 5;
increment(a);
std::cout << a << "\n"; // 6
```

- More efficient for large objects (no copy)
    
- Caller’s object can be modified (unless using `const` references)
    

### Reference Return Types

A function can return a reference to allow modifications or avoid copying large objects.

```cpp
int& getElement(std::vector<int>& v, size_t idx) {
    return v[idx]; // returns reference to element
}

std::vector<int> data = {10, 20, 30};
getElement(data, 1) = 25; // modifies data[1]
```

**Warning:** Returning references to local variables is illegal (dangling reference). Only return references to objects that outlive the function call.

---

## Rvalue References (C++11)

Rvalue references (type `T&&`) can bind to **temporary (rvalue) objects** that typically have no persistent address. Introduced in C++11, they enable _move semantics_ and more advanced patterns.

### Syntax and Semantics

```cpp
int&& r = 10; // r is an rvalue reference bound to temp 10
r = 20; // modifies that temporary object (still in scope until statement ends)
```

Rvalue references can bind to **rvalue expressions** (e.g., temporaries, results of expressions) not bound by lvalue references.

### Move Semantics

With move semantics, resources can be transferred from one object to another rather than copied.

```cpp
std::vector<int> makeVector() {
    std::vector<int> tmp{1,2,3};
    return tmp; // Named Return Value Optimization or Move
}

std::vector<int> v = makeVector();

// Example move constructor
MyClass(MyClass&& other) {
    this->ptr = other.ptr;
    other.ptr = nullptr;
}
```

### Perfect Forwarding

Enables writing template functions that can forward arguments while preserving whether they’re lvalues or rvalues:

```cpp
template<typename T, typename... Args>
std::unique_ptr<T> make(Args&&... args) {
    return std::unique_ptr<T>(new T(std::forward<Args>(args)...));
}
```

This is critical for factory functions, container emplace operations, etc.

---

## Reference Binding Rules

### Lvalue Reference Binding

- `T&` binds to an lvalue of type `T` (or derivable). E.g., `int&` can bind to an `int` lvalue.
    
- Cannot bind directly to a temporary.
    

### Const Lvalue Reference Binding

- `const T&` can bind **both** to lvalues and **rvalues** (including temporaries). This extends the temporary’s lifetime.
    

```cpp
const int& cr = 10; // legal
```

### Rvalue Reference Binding

- `T&&` can bind to rvalues. A `std::move(x)` casts `x` to an xvalue (treated like an rvalue), allowing rvalue references to bind.
    

---

## Reference Lifetime Extension

If a reference is bound to a temporary, the lifetime of that temporary is **extended** to match the lifetime of the reference, _if_ it’s a const or rvalue reference.

```cpp
const std::string& strRef = std::string("temp");
// the temporary std::string lives as long as strRef
std::cout << strRef << "\n"; // valid
```

But be careful: binding to a `const` reference or an rvalue reference can lead to confusion if the object is used beyond that scope.

---

## Reference to Reference Collapsing Rules

When references to references occur through templates or typedefs, the compiler applies _reference collapsing_:

|Expression|Result|
|---|---|
|`T& &`|`T&`|
|`T& &&`|`T&`|
|`T&& &`|`T&`|
|`T&& &&`|`T&&`|

### Forwarding References (Universal References)

A function template parameter of the form `T&&` where `T` is deduced can become either an lvalue or rvalue reference depending on the argument, known as _forwarding references_.

```cpp
template<typename T>
void foo(T&& x) {
    bar(std::forward<T>(x));
}
```

This is the foundation of perfect forwarding.

---

## References vs Pointers

|Aspect|Reference|Pointer|
|---|---|---|
|Null/None|Cannot be null|Can be null (or invalid)|
|Syntax|`T& ref = obj;`|`T* ptr = &obj;`|
|Rebind|Cannot be reseated|Can be changed to point elsewhere|
|Implementation|Often no extra size|Typically stores an address|
|Indirection|`ref` => direct usage|`*ptr` to dereference|

### Tradeoffs and Selection Criteria

- Use references when **binding** a function parameter to a guaranteed valid object.
    
- Use pointers when **null** states, dynamic re-seating, or pointer arithmetic are required.
    
- Prefer **const references** for read-only access and no copying overhead.
    

---

## Dangling References

Occur when a reference outlives the object it refers to:

```cpp
int& badRef() {
    int x = 10;
    return x; // x is destroyed => dangling reference
}

int main() {
    int& r = badRef(); // invalid use
}
```

Always ensure the referenced object’s lifetime _exceeds_ that of the reference.

---

## std::reference_wrapper (C++11)

`std::reference_wrapper<T>` provides a copyable, assignable wrapper around a reference. Useful for storing references in containers that normally require copyable objects.

```cpp
std::vector<std::reference_wrapper<int>> refs;
int a=1,b=2;
refs.push_back(a);
refs.push_back(b);

refs[0].get() = 10; // modifies a
```

---

## References in Range-for Loops

Reference types in range-based `for` can avoid copying:

```cpp
std::vector<std::string> words = {"hi","bye"};

// Copy each string
for (auto w : words) {
    w += "!"; // modifies local copy
}

// Use reference to modify original
for (auto& w : words) {
    w += "?"; // modifies original
}

// Use const reference to read without copying
for (const auto& w : words) {
    std::cout << w << " ";
}
```

---

## Structured Bindings (C++17)

Structured bindings let you decompose objects into named references:

```cpp
std::pair<int, std::string> p{42, "answer"};

auto& [num, text] = p; // references to p.first and p.second
num++; // modifies p.first
std::cout << p.first << "\n"; // 43
```

If you want them to be non-references, omit `&`, which copies, or use `const auto&` to bind references to const.

---

## Lifetime Issues with References

### References to Temporary Objects

When you bind a temporary to a const reference or rvalue reference, the temporary’s lifetime is extended, but only until the **reference goes out of scope**.

```cpp
const std::string& ref = std::string("temp"); // extends lifetime until scope ends
std::cout << ref << "\n"; // safe
```

Be cautious about returning references to local objects or storing references in long-lived structures to short-lived objects.

---

**Conclusion**: C++ references provide a powerful mechanism to alias existing objects or enable advanced idioms like move semantics and perfect forwarding. Use lvalue references for parameter passing and read/write aliases, rvalue references for move operations, and be mindful of lifetimes to avoid dangling references.