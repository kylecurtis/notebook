# Smart Pointers in C++

Smart pointers encapsulate ownership of dynamically allocated objects, ensuring proper deallocation while reducing the risk of memory leaks and dangling pointers. They come in various forms—unique, shared, and weak—each serving different ownership semantics.

```cpp
#include <memory>   // For std::unique_ptr, std::shared_ptr, etc.
#include <iostream>
#include <string>
#include <vector>
```

---

## std::unique_ptr (C++11)

`std::unique_ptr<T>` is a smart pointer that expresses **exclusive ownership** of a dynamically allocated object.

### Ownership Semantics

- Exactly one `std::unique_ptr` can own a given object at a time.
    
- When it goes out of scope, it deletes the managed object.
    
- It cannot be copied, only moved.
    

```cpp
std::unique_ptr<int> ptr1(new int(10));
// std::unique_ptr<int> ptr2 = ptr1; // Error: cannot copy
```

### Move Operations

`std::unique_ptr` can be transferred via **move semantics**:

```cpp
std::unique_ptr<int> ptr1(new int(10));
std::unique_ptr<int> ptr2 = std::move(ptr1); // ptr1 becomes nullptr
```

### Custom Deleters

You can provide a **custom deleter** function or functor:

```cpp
struct Deleter {
    void operator()(int* p) {
        std::cout << "Deleting int\n";
        delete p;
    }
};

std::unique_ptr<int, Deleter> up(new int(5), Deleter());
```

Useful for logging, resource cleanup, or specialized memory management.

### Array Support

For arrays, use `std::unique_ptr<T[]>`:

```cpp
std::unique_ptr<int[]> arr(new int[10]);
arr[0] = 42;
```

### Making Non-copyable Resources

`std::unique_ptr` helps represent resources that shouldn’t be duplicated. Good for file handles, sockets, or dynamically allocated objects that must not be shared.

---

## std::shared_ptr (C++11)

`std::shared_ptr<T>` is a reference-counted smart pointer that allows **shared ownership** of an object.

### Reference Counting

- Multiple `std::shared_ptr`s can point to the same object.
    
- The object is destroyed when the **last** `std::shared_ptr` goes out of scope.
    

```cpp
std::shared_ptr<int> sp1(new int(42));
{
    std::shared_ptr<int> sp2 = sp1; // now reference count is 2
} // sp2 goes out of scope, count back to 1
// object is destroyed when sp1 also goes out of scope
```

### Thread Safety Guarantees

- Multiple threads can read/write to **distinct** `std::shared_ptr` objects that share the same data safely.
    
- Atomic operations on the internal reference count.
    
- Modifications to a single shared_ptr instance require external synchronization if accessed by multiple threads.
    

### Control Block Structure

Each `std::shared_ptr` has a _control block_ that stores:

1. **Pointer** to the managed object
    
2. **Reference count**
    
3. **Weak count** (for `std::weak_ptr`)
    
4. Optional **custom deleter**
    

### Custom Deleters

Similar to `unique_ptr`, can have a custom deleter. This is stored in the control block.

```cpp
auto deleter = [](Foo* p){
    std::cout << "Deleting Foo\n";
    delete p;
};
std::shared_ptr<Foo> sp(new Foo, deleter);
```

### Aliasing Constructor

`std::shared_ptr` has an aliasing constructor that allows two shared pointers to share the same control block but point to different sub-objects:

```cpp
struct S {
    int x;
};

std::shared_ptr<S> sptr(new S{10});
// aliasing: both share control block, but myPtr points to sptr->x
std::shared_ptr<int> myPtr(sptr, &sptr->x);
```

### create_shared (C++20)

Enables constructing a `std::shared_ptr` from an already existing object but with an internal reference count. The object is not allocated by the system.

```cpp
S s{10};
std::shared_ptr<S> sp = std::create_shared(&s); // C++20
```

### make_shared Optimization

`std::make_shared<T>(args...)` allocates the **object** and **control block** in a single memory allocation, improving performance and memory usage.

```cpp
auto sp = std::make_shared<int>(42);
```

---

## std::weak_ptr (C++11)

`std::weak_ptr<T>` is a **non-owning** reference to an object managed by `std::shared_ptr`. It doesn’t affect the reference count.

### Breaking Cyclic Dependencies

Cyclic references between shared pointers cause memory leaks if they keep each other alive. Using `std::weak_ptr` on one side of the cycle breaks it.

### Expired Pointers

A weak pointer can **expire** if the managed object is destroyed. Checking:

```cpp
std::weak_ptr<int> wp = sp; // sp is a shared_ptr<int>
if (auto locked = wp.lock()) {
    // locked is a std::shared_ptr<int> if not expired
}
```

### Lock Mechanism

`wp.lock()` returns a `std::shared_ptr<T>` if the object is still alive, or an empty `shared_ptr` if expired.

### weak_from_this (C++17)

Allows an object that inherits from `std::enable_shared_from_this` to get a `weak_ptr` to itself. Useful for referencing itself weakly.

---

## std::auto_ptr (Deprecated)

### Historical Context

`std::auto_ptr` (C++98) was the precursor to `unique_ptr`. Its copy semantics were unintuitive (transferring ownership on copy) and has been removed in C++17.

### Migration to unique_ptr

Replace `auto_ptr<T>` with `std::unique_ptr<T>`. The latter has well-defined move semantics.

---

## std::observer_ptr (Library TS)

A proposed non-owning pointer wrapper that simply indicates no ownership. Not in standard as of C++20, but in the **Library Fundamentals TS**. Serves as a clear marker of non-owning references.

---

## Intrusive Pointer Alternatives

Intrusive reference counting stores ref counts **inside** the managed object. For example, `boost::intrusive_ptr`. The object must expose methods to increment/decrement counts.

---

## Custom Smart Pointers

### Implementing Reference Counting

You can create a custom smart pointer that increments a counter on copy, decrements on destruction, and frees the object when the count hits zero. Make sure to handle threads if concurrency is needed.

### Custom Ownership Models

- **Borrowed references**: external lifetime management.
    
- **Link counting**: advanced or specialized reference counting.
    
- **Shared but immovable** resources.
    

---

## Smart Pointer Performance Considerations

- **make_shared**: single allocation for object + control block => improved cache locality.
    
- **shared_ptr** overhead**: atomic increments/decrements of refcount.
    
- **unique_ptr** is zero-overhead once inlined, except for the pointer storage.
    
- Memory overhead for control blocks.
    

---

## Smart Pointer Best Practices

1. **Use `std::unique_ptr`** by default for exclusive ownership.
    
2. **Use `std::shared_ptr`** for shared ownership, but be mindful of reference cycles.
    
3. **Avoid raw pointers** for ownership; prefer them for non-owning references.
    
4. **Use `std::weak_ptr`** to break cycles or observe an object’s lifetime.
    
5. **Use custom deleters** for resource cleanup beyond `delete`.
    
6. **Avoid `new`/`delete`** in user code directly; prefer `make_shared` or `make_unique`.
    

---

## Smart Pointers with Incomplete Types

You can declare `std::unique_ptr<ForwardDecl>` to a forward-declared class if you only use it in places that don’t require the class definition (e.g., as a function parameter or member variable). The destructor still needs a complete type if it’s inlined.

---

## Smart Pointers for Arrays

- **`std::unique_ptr<T[]>`** can manage arrays. You can use `.get()[index]` or the subscript operator on `unique_ptr<T[]>`.
    
- **`std::shared_ptr<T>`** with a custom deleter can also manage arrays, but less typical.
    
- **Prefer `std::vector`** for dynamic arrays, as it handles resizing and avoids manual memory.
    

---

## Using Smart Pointers in APIs

- Functions that consume an object might take `std::unique_ptr<T>` by value, signifying transfer of ownership.
    
- Functions that share ownership might take or return `std::shared_ptr<T>`.
    
- Non-owning references are best expressed with raw pointers or references, or `std::weak_ptr<T>` if linked to a `std::shared_ptr<T>`.
    

---

**In conclusion**, modern C++ heavily relies on smart pointers (`std::unique_ptr`, `std::shared_ptr`, and `std::weak_ptr`) to manage dynamic lifetimes safely. They reduce manual memory management and the risk of leaks or dangling pointers, providing well-defined ownership semantics that scale to complex scenarios.