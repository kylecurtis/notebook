# Classes Fundamentals in C++

C++ classes encapsulate data (members) and functions (methods), forming the basis of **object-oriented** programming. Structs and classes share many properties but differ mainly by default access specifiers.

```cpp
#include <iostream>
#include <string>
```

---

## Class Definition Syntax

```cpp
// Example class definition
class MyClass {
public:
    MyClass();             // constructor
    void doSomething();    // member function

private:
    int value;             // private data member
};
```

- **Keyword**: `class` or `struct`
    
- **Access specifiers**: `public:`, `protected:`, `private:`
    
- **Semicolon** at the end of the class definition.
    

---

## Class vs Struct

- In C++, **struct** defaults to **public** members, and **class** defaults to **private**.
    
- Otherwise, they are nearly identical in capabilities.
    

```cpp
struct Point {
    int x;
    int y;
};

// By default, x,y are public in struct.
```

Use `class` for object-oriented designs, `struct` often for simple data aggregates.

---

## Data Members

### Instance Variables

Each object instance has its own copy of the data members. E.g., `value` in `MyClass` above.

```cpp
class Counter {
public:
    void increment() { ++count; }
private:
    int count = 0; // instance variable
};
```

### Static Members

Shared among **all** instances, one per class.

```cpp
class Foo {
public:
    static int globalCount; // declaration
};

int Foo::globalCount = 0; // definition outside class
```

Accessed via `Foo::globalCount` or object references.

### Member Initialization

1. **In-class initializers** (C++11): `int count = 0;`
    
2. **Constructor initialization list**:
    

```cpp
class Bar {
public:
    Bar() : x(10), y(20) {}
private:
    int x;
    int y;
};
```

### Member Ordering

- Members are typically laid out in declared order, though alignment can introduce padding.
    
- Initialization occurs in the order of declaration, not the order in the constructor’s init list.
    

---

## Member Functions

### Instance Methods

Regular functions that operate on a specific object.

```cpp
class Widget {
public:
    void update() {
        // uses instance data
        data++;
    }
private:
    int data = 0;
};
```

### const Member Functions

Cannot modify the object’s state, unless members are declared `mutable`.

```cpp
class C {
public:
    int getValue() const {
        // cannot modify non-mutable data
        return value;
    }
private:
    int value;
};
```

### Static Member Functions

- Do not have a `this` pointer.
    
- Only access static members or data passed in.
    

```cpp
class Math {
public:
    static int add(int a, int b) {
        return a + b;
    }
};

int s = Math::add(3,4);
```

### Member Function Overloading

Multiple member functions with the same name but different parameter lists.

```cpp
class Overloaded {
public:
    void set(int v);
    void set(std::string v);
};
```

### this Pointer

A hidden parameter in each non-static member function, pointing to the current object.

```cpp
class Self {
public:
    void show() {
        std::cout << "Address: " << this << "\n";
    }
};
```

#### Explicit vs Implicit this

- **Implicit** usage: `value = 10; // same as this->value = 10;`
    
- **Explicit** usage: `this->value = 10;`
    

#### this Type Variations

- In a `const` member function, `this` is a pointer to a **const** object (`const Self* const`).
    
- In an rvalue reference qualified method (`&&`), `this` is a pointer to an _xvalue_.
    

---

## Access Specifiers

### public

Members accessible **everywhere**.

### protected

Members accessible by **this class** and **derived classes**, but not outside.

### private

Accessible only by **this class** itself (and friends).

### Access Control Strategies

- Data Hiding: keep implementation details in private/protected.
    
- Provide public methods to manipulate data.
    

---

## Friend Declaration

A **friend** can access private/protected members.

### Friend Functions

```cpp
class MyClass {
    friend void func(MyClass& m); // friend function
private:
    int secret;
};

void func(MyClass& m) {
    m.secret = 42; // allowed
}
```

### Friend Classes

One class can declare another as a friend.

```cpp
class A {
    friend class B;
private:
    int x;
};

class B {
    void accessA(A& a) {
        a.x = 10; // allowed
    }
};
```

### Friend Member Functions

You can also befriend only specific member functions of another class.

---

## Member Types (Nested Types)

Classes can declare **nested classes**, `using` aliases, or enums.

```cpp
class Outer {
public:
    class Inner {
        // ...
    };
};
```

### Local Classes

A class defined **inside a function**. Rarely used but valid.

### Anonymous Classes

C++ allows anonymous structs/classes as members in some contexts (primarily for C compatibility).

### Class Forward Declarations

Let you declare a class name without defining its contents, enabling references/pointers to incomplete types.

```cpp
class Forward;
Forward* f; // okay, can’t use f’s members yet
```

### Member Access Control

Nested classes can be private/protected, controlling who can see them.

---

## Size and Layout of Classes

### Alignment Issues

Struct/class members are aligned according to their types. The compiler may insert **padding**.

### Padding Optimization

Member ordering can reduce padding:

```cpp
// Good alignment
class Example {
    int a;
    int b;
    char c;
    char d;
};
```

### Empty Base Optimization

If a class inherits from an empty base, the compiler can optimize away the base’s size (permitted by the standard). Helps with certain patterns like CRTP.

---

## Most Vexing Parse Problem

An infamous parsing ambiguity where something that looks like an object definition could be interpreted as a function declaration.

```cpp
// Example
Widget w(Widget()); // can be parsed as a function prototype!
```

Use braces or additional parentheses to disambiguate. The issue is mostly historical and arises from C++ grammar.

---

**Conclusion**: C++ classes/structs are a cornerstone of the language’s OOP features, supporting encapsulation, access control, static vs. per-object data, and flexible function overloading. Understanding layout, initialization, and the this pointer is critical for writing robust class-based designs.