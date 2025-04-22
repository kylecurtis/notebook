# Constructors and Initialization in C++

Constructors are special member functions that control how objects of a class are **initialized**. C++ offers various constructor forms—default, copy, move, etc.—plus language features to manage initialization order and resource handling.

```cpp
#include <iostream>
#include <string>
#include <vector>
```

---

## Default Constructor

A **default constructor** is one that can be called with no arguments. It can be either **implicitly** provided by the compiler or **user-defined**.

```cpp
class A {
public:
    A() { // user-defined default constructor
        std::cout << "A default constructor\n";
    }
};
```

### Implicit vs Explicit Default Constructor

- **Implicit**: If you provide no constructors at all, the compiler generates a default constructor (only if needed).
    
- **Explicit**: You can write `A() = default;` or implement it yourself.
    

### defaulted Constructor (C++11)

```cpp
class B {
public:
    B() = default; // explicitly request a default constructor
    // ...
};
```

Use when you need a default constructor but also have other constructors or want to override a suppressed one.

---

## Parameterized Constructors

Constructors that take arguments:

```cpp
class Point {
public:
    Point(int xVal, int yVal) : x(xVal), y(yVal) {
        std::cout << "Constructing Point(" << xVal << ", " << yVal << ")\n";
    }
private:
    int x;
    int y;
};
```

---

## Copy Constructor

### Default Copy Behavior

If you don’t provide a copy constructor, the compiler generates one that performs a **memberwise copy**.

```cpp
class C {
    // implicit copy constructor does: copy data from each member
};
```

### Defining Custom Copy Constructors

You can define your own to customize the copy process (e.g., deep copy dynamic memory).

```cpp
class Array {
public:
    Array(const Array& other) {
        // deep copy
    }
};
```

### Preventing Copying

Use `= delete` in C++11:

```cpp
class NonCopy {
public:
    NonCopy(const NonCopy&) = delete; // disallow copying
    NonCopy& operator=(const NonCopy&) = delete;
};
```

### Shallow vs Deep Copy

- **Shallow copy**: copy pointer values, share underlying data.
    
- **Deep copy**: allocate new memory and duplicate data.
    

### Copy Elision

The compiler can **omit** creating temporary objects in some contexts (return statements, exception throwing), called **(Named) Return Value Optimization**. Minimizes copy overhead.

---

## Move Constructor (C++11)

### Move Semantics

Allows transferring resources from a **temporary** or an object that is about to be destroyed. Instead of copying, ownership is moved.

```cpp
class M {
public:
    M(M&& other) {
        // "steal" resources from other
        other.ptr = nullptr;
    }
};
```

### noexcept Move Operations

Mark move constructor as `noexcept` if it truly cannot throw. Encourages use in standard library optimizations.

```cpp
M(M&& other) noexcept {
    // ...
}
```

### Implementing Efficient Moves

Use move semantics for large data structures (e.g., vectors). Transfer pointers instead of copying entire contents.

---

## Converting Constructors

Constructors that can be called with a single argument are **converting** (e.g., `String(const char*)`).

### explicit Keyword

Prevents implicit conversions:

```cpp
class X {
public:
    explicit X(int n) { /* ... */ }
};

X x1 = 10;      // error if constructor is explicit
X x2(10);       // ok
```

### Conversion Operators

Operators like `operator int()` or `operator std::string()` let objects be used in expressions requiring another type.

```cpp
class C {
public:
    operator int() const { return value; }
private:
    int value;
};
```

---

## Delegating Constructors (C++11)

A constructor can call another constructor in its initialization list:

```cpp
class D {
public:
    D() : D(42) { // delegate to D(int)
        std::cout << "default\n";
    }
    D(int x) {
        std::cout << "int\n";
    }
};
```

---

## Inheriting Constructors (C++11)

Derived classes can **inherit** base class constructors:

```cpp
struct Base {
    Base(int x) {}
};

struct Derived : Base {
    using Base::Base; // inherit Base(int) constructor
};
```

---

## In-class Member Initializers (C++11)

Initialize members where they’re declared:

```cpp
class E {
private:
    int x = 10; // in-class initializer
public:
    E() {} // x is 10 by default
};
```

---

## Member Initialization List

Use an **initialization list** to initialize data members before the constructor body:

```cpp
class F {
public:
    F(int a, int b) : x(a), y(b) {
        // constructor body
    }
private:
    int x;
    int y;
};
```

### Initialization Order

Members are initialized **in the order of their declaration**, not the order in the list.

### Performance Implications

Initialization is generally cheaper than default-construct-then-assign in the constructor body.

### Initialization vs Assignment

Assigning in the constructor body calls default constructor first, then assignment. Initialization list directly constructs the object.

---

## Initialization Order Across Translation Units

Static/global objects in different translation units can have unspecified initialization order. Avoid relying on cross-TU initialization timing (use function-level static or design patterns like the Singleton pattern carefully).

---

## Constructor Overloading

Multiple constructors with different parameter lists.

```cpp
class Over {
public:
    Over() {}
    Over(int) {}
    Over(std::string) {}
};
```

### Perfect Forwarding Constructors

Template constructors that forward arguments to another constructor, preserving lvalue/rvalue-ness.

```cpp
template<typename... Args>
Foo(Args&&... args) : Foo(std::forward<Args>(args)...) {}
```

---

## Private Constructors

Constructors can be private to prevent direct instantiation. Common in **Singleton** or factory patterns.

### Factory Methods

A static function in the class returns an instance.

```cpp
class G {
private:
    G() {}
public:
    static G create() { return G(); }
};
```

### Named Constructor Idiom

Use static methods with descriptive names instead of multiple constructors.

```cpp
class H {
private:
    H(int x) {}
public:
    static H fromInt(int x) {
        return H(x);
    }
    static H defaultH() {
        return H(0);
    }
};
```

---

**Conclusion**: Mastering constructors in C++ is crucial for proper resource management, performance, and clarity. Modern features like **move constructors**, **in-class initializers**, and **delegating** or **inheriting** constructors simplify code while maintaining efficiency.