# Dynamic Memory Management in C++

Dynamic memory allocation in C++ provides flexible control over object lifetimes, sizes, and allocation strategies. However, it also introduces risks like memory leaks and corruption. This guide covers the standard **new/delete** operators, custom allocators, memory alignment, and debugging techniques.

```cpp
#include <iostream>
#include <cstdlib>   // For malloc/free, aligned_alloc
#include <new>       // For std::nothrow, placement new
#include <memory>    // For smart pointers
#include <vector>
```

---

## Memory Allocation Functions

### malloc/free vs new/delete

- `malloc()`/`free()` are **C-style** allocation functions. They allocate or deallocate raw memory but **do not** call constructors or destructors.
    
- `new` calls both **allocation** and **constructor**, while `delete` calls **destructor** then frees memory.
    

```cpp
// Using malloc/free
int* cptr = (int*)std::malloc(sizeof(int)*10);
if (!cptr) {
    // handle allocation failure
}
std::free(cptr);

// Using new/delete
int* nptr = new int(5); // calls constructor of int (trivial in this case)
std::cout << *nptr << "\n";
delete nptr; // calls destructor, then frees memory
```

- Prefer `new/delete` for C++ objects. `malloc/free` is rarely used in modern C++ except for low-level or legacy code.
    

### new/delete Operators

- **`new`** allocates memory on the free store and returns a pointer to the constructed object.
    
- **`delete`** destroys the object (calls destructor) and frees the memory.
    

```cpp
class Foo {
public:
    Foo() { std::cout << "Foo constructed\n"; }
    ~Foo() { std::cout << "Foo destroyed\n"; }
};

Foo* fooPtr = new Foo; // calls Foo::Foo()
delete fooPtr;         // calls Foo::~Foo() then frees memory
```

### new[]/delete[] for Arrays

- Use **`new[]`** for dynamically allocated arrays, and **`delete[]`** to deallocate.
    

```cpp
int* arr = new int[10]; // allocate array of 10 ints
// ... use arr[0..9]

delete[] arr; // must use delete[]
```

- Failing to use matching `delete[]` on an array allocated with `new[]` leads to undefined behavior.
    

### nothrow new

- `new` throws `std::bad_alloc` on failure by default.
    
- **nothrow new** returns `nullptr` instead of throwing.
    

```cpp
int* p = new(std::nothrow) int[100000000];
if (!p) {
    // handle allocation failure
}
```

### Placement new

- Allows constructing an object **at a specific memory address** (no allocation occurs).
    
- Usually used in custom allocators or to construct objects in pre-allocated buffers.
    

```cpp
#include <new>

void* buffer = std::malloc(sizeof(Foo));
Foo* pFoo = new(buffer) Foo; // placement new in buffer
// ... use *pFoo
pFoo->~Foo(); // manually call destructor
std::free(buffer);
```

---

## Custom Memory Allocation

### Constructing in Pre-allocated Memory

1. Allocate raw memory (e.g., via `malloc`, `aligned_alloc`, or custom memory pool).
    
2. Construct objects **in place** using placement new.
    
3. Call destructors manually.
    
4. Free raw memory.
    

### In-place Construction

Similar to the above, just note you are **reusing** an already allocated block:

```cpp
char rawMemory[sizeof(int)*5];
int* arr = reinterpret_cast<int*>(rawMemory);

for (int i = 0; i < 5; ++i) {
    new(&arr[i]) int(i*10); // construct int in place
}

// Destruction
for (int i = 0; i < 5; ++i) {
    arr[i].~int();
}
```

---

## Custom Memory Management

### Overloading new/delete

C++ allows **overloading global** or **class-specific** `new`/`delete` operators.

- **Global**: Affects all calls to `new` in the program (unless overshadowed by class-specific versions).
    
- **Class-specific**: Only for objects of that class.
    

### Class-specific new/delete

```cpp
struct MyClass {
    static void* operator new(std::size_t sz) {
        std::cout << "MyClass custom new\n";
        return ::operator new(sz); // calls global operator new
    }
    static void operator delete(void* ptr) {
        std::cout << "MyClass custom delete\n";
        ::operator delete(ptr);
    }
};

MyClass* p = new MyClass; // calls MyClass::operator new
delete p;                 // calls MyClass::operator delete
```

### Global new/delete

```cpp
void* operator new(std::size_t sz) {
    std::cout << "Global custom new(" << sz << ")\n";
    void* mem = std::malloc(sz);
    if (!mem) throw std::bad_alloc();
    return mem;
}

void operator delete(void* ptr) noexcept {
    std::cout << "Global custom delete\n";
    std::free(ptr);
}
```

Used rarely in specialized systems, or for debugging allocation patterns.

---

## Memory Allocation Patterns

### POD Allocators

Allocate **Plain Old Data** blocks for trivial types. Usually a custom scheme for homogeneous data structures.

### Object Pools

Keep a pool of pre-allocated objects to avoid frequent allocations.

```cpp
class ObjectPool {
    // Implementation that caches a certain number of objects
};
```

### Arena/Region Allocators

Allocate large chunks (“arenas”) at once. Individual objects are constructed in the arena. Freed all at once when the arena is destroyed.

### Stack Allocators

Allocate from a stack-like structure. Freed in LIFO order.

### Buddy System

Divide memory into power-of-two sized blocks. Combine or split blocks as needed. Less common in standard user-space code.

---

## Memory Alignment

### alignas Specifier (C++11)

For specifying stricter alignment than default.

```cpp
struct alignas(16) Vector4 {
    float x, y, z, w;
};
Vector4 v; // guaranteed 16-byte alignment
```

### aligned_alloc (C++17)

Allocates memory with specified alignment.

```cpp
#include <cstdlib>

void* ptr = std::aligned_alloc(64, 1024); // 64-byte alignment, 1024 bytes
std::free(ptr);
```

### Over-aligned Types

Types with alignment stricter than the default platform alignment. Must ensure appropriate alignment in custom allocators.

---

## Memory Access Patterns

### Cache-friendly Access

- Contiguous data (e.g., arrays) is typically more cache-friendly than linked structures.
    
- Align data on cache-line boundaries for performance gains in tight loops.
    

### False Sharing Avoidance

- Occurs when two threads modify different data in the same cache line.
    
- Pad or align data to separate cache lines.
    

---

## Memory Leaks

A **memory leak** occurs when allocated memory is never freed, making it inaccessible.

### Detection Techniques

- Tools like **Valgrind**, **AddressSanitizer**, or built-in OS debuggers.
    
- Instrumentation or custom allocators that track allocations.
    

### Prevention Strategies

- Prefer **smart pointers** (`std::unique_ptr`, `std::shared_ptr`) over raw pointers.
    
- RAII: allocate in constructor, deallocate in destructor.
    
- Use containers (`std::vector`, `std::string`) instead of manual arrays.
    

### Tools for Analysis

- **Valgrind** (Linux), **Dr. Memory**, or **Visual Studio Memory Diagnostics**.
    
- **LeakSanitizer** (part of Clang’s sanitizers).
    

---

## Memory Corruption

### Buffer Overflows

Writing beyond array boundaries can overwrite unrelated memory.

### Use-after-free

Dereferencing a pointer after `delete` is undefined behavior.

### Double-free

Calling `free` or `delete` on the same pointer more than once.

### Memory Debugging Tools

- **AddressSanitizer**: detects out-of-bounds, use-after-free, etc.
    
- **Electric Fence**: guards memory with protected pages.
    
- **Valgrind**: memory check tool.
    

---

**In summary**, dynamic memory management in C++ is flexible but requires careful use of **new/delete** or custom allocation patterns to avoid leaks and corruption. Prefer modern approaches like **smart pointers** and **STL containers** wherever possible for safer, more maintainable code.