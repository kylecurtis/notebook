## 1. Core Language Basics

1. **Syntax & Basic Types**
    
    - Fundamental data types (integral, floating, `bool`, `char`, etc.)
        
    - Declarations vs. definitions, scope, name hiding
        
    - Arrays vs. pointers
        
2. **Control Flow**
    
    - if/else, switch, loops (for, while, do-while), range-based for
        
    - Understanding of short-circuit evaluation, break/continue, goto
        
3. **Functions**
    
    - Pass-by-value vs pass-by-reference, default arguments, function overloading
        
    - Inline functions, const-correctness, function pointers
        
4. **Compilation Model**
    
    - Headers vs. source files, includes, forward declarations
        
    - Object files, linking, the One Definition Rule (ODR)
        

**Why:** Every C++ job expects you to write clear, basic C++ code and understand the compilation model.

---

## 2. Object-Oriented Programming

1. **Classes vs Structs**
    
    - Encapsulation, default access specifiers
        
    - Data members vs. member functions
        
2. **Access Specifiers**
    
    - public, private, protected
        
    - friend classes/functions
        
3. **Inheritance & Polymorphism**
    
    - Base vs. derived classes, virtual functions, overrides, pure virtual
        
    - Run-time vs. compile-time polymorphism (templates)
        
4. **Abstract Classes & Interfaces**
    
    - Virtual destructors, pure virtual methods
        
5. **Multiple Inheritance & Virtual Base Classes** (less common, but can appear in older code)
    
6. **Object Lifetime**
    
    - Construction, destruction, RAII
        

**Why:** Many interview questions revolve around understanding how OOP is done in C++, especially with the complexities of virtual functions and memory management.

---

## 3. Memory Management

1. **Stack vs. Heap Allocation**
    
    - Automatic vs. dynamic storage duration
        
    - `new`/`delete`, `malloc`/`free` (legacy vs. idiomatic usage)
        
2. **Pointers & References**
    
    - Pointer arithmetic, nullptr, reference binding rules
        
    - Dangling pointers, pointer validity
        
3. **Ownership Semantics**
    
    - RAII (Resource Acquisition Is Initialization)
        
    - `unique_ptr`, `shared_ptr`, `weak_ptr`, custom deleters
        
4. **Dynamic Arrays**
    
    - `new[]`/`delete[]`, or `std::vector` in modern code
        
    - Avoiding memory leaks
        
5. **Smart Pointers (C++11+)**
    
    - `std::unique_ptr`, `std::shared_ptr`, `std::weak_ptr`, how reference counting works
        
    - Circular references, breaking cycles
        
6. **Allocators & Custom Allocation**
    
    - Overloading `new`/`delete`, pool allocators, arena allocators
        

**Why:** Memory management is a foundation of C++; interviewers expect you to handle dynamic memory safely, and know modern alternatives.

---

## 4. Constructors & Object Initialization

1. **Constructor Types**
    
    - Default, copy, move, conversion, delegating, inheriting
        
    - `explicit` keyword
        
    - `= default`, `= delete`
        
2. **Initialization Details**
    
    - Member initializer lists vs. assignment
        
    - Order of initialization, default member initializers
        
3. **Copy & Move Semantics**
    
    - Deep vs. shallow copy, move semantics for performance
        
    - Rvalue references, move constructors/operators
        
4. **RAII**
    
    - Resource acquisition in constructors, release in destructors
        

**Why:** Ensuring correct, efficient object creation is critical to building robust libraries and apps.

---

## 5. Templates & Generic Programming

1. **Function Templates & Class Templates**
    
    - Template parameters, instantiation, specialization
        
    - Understanding how the compiler instantiates templates
        
2. **Variadic Templates (C++11+)**
    
    - Parameter packs, `std::forward`, perfect forwarding
        
3. **SFINAE (Substitution Failure Is Not An Error)**
    
    - Basic idea behind advanced template metaprogramming
        
    - `std::enable_if`, `std::is_same`, type traits
        
4. **Template Specialization**
    
    - Partial vs. full specialization
        
    - Overloading vs. specialization pitfalls
        
5. **Compile-Time Programming**
    
    - `constexpr` functions, type traits, template metaprogramming
        

**Why:** Many advanced C++ libraries use templates heavily for performance and genericity. Interviews often test if you understand template basics.

---

## 6. The Standard Library

1. **Containers**
    
    - `std::vector`, `std::array`, `std::deque`, `std::list`, `std::forward_list`, `std::map`, `std::unordered_map`, `std::set`, etc.
        
    - Complexity guarantees, when to use which container
        
2. **Iterators & Algorithms**
    
    - Ranges over containers, `std::begin`, `std::end`
        
    - `std::sort`, `std::find`, `std::accumulate`, `std::transform`, etc.
        
    - Iterator categories (random access, bidirectional, input, output)
        
3. **Strings**
    
    - `std::string`, `std::wstring`, string operations
        
    - Common pitfalls (e.g. implicit conversions, `c_str()` usage)
        
4. **Function Objects & Lambdas**
    
    - Syntax, captures, mutable lambdas
        
5. **Smart Pointers**
    
    - `std::unique_ptr`, `std::shared_ptr`, `std::weak_ptr` (mentioned above)
        
6. **Utility Components**
    
    - `std::pair`, `std::tuple`, `std::optional` (C++17), `std::variant` (C++17), `std::any` (C++17)
        
7. **Time, Date, and Chrono**
    
    - `std::chrono`, steady clocks, durations
        
8. **I/O Streams**
    
    - `std::cin`, `std::cout`, string streams, file streams
        

**Why:** Standard library knowledge is often tested; it’s essential for practical development. Interviewers frequently ask about container choices and complexities.

---

## 7. Concurrency & Multithreading (C++11+)

1. **Threads**
    
    - `std::thread`, launching/joining threads, concurrency
        
2. **Mutexes & Locks**
    
    - `std::mutex`, `std::lock_guard`, `std::unique_lock`, condition variables
        
3. **Atomics**
    
    - `std::atomic`, memory ordering, CAS (compare-and-swap)
        
4. **Futures & async**
    
    - `std::async`, `std::future`, `std::promise`
        
5. **Parallel Algorithms (C++17)**
    
    - Execution policies, parallel STL
        

**Why:** Modern C++ often involves concurrency. Many roles require knowledge of safe multi-threaded programming and synchronization.

---

## 8. Advanced Topics & Language Features

1. **Move-Only & Reference-Only Types**
    
    - RAII classes that are non-copyable
        
2. **constexpr (C++11+)**
    
    - Compile-time evaluation, literal types
        
3. **Operators Overloading**
    
    - Arithmetic, comparison, assignment, subscript, function call operator
        
4. **Name Lookup, ADL (Argument-Dependent Lookup)**
    
    - Understanding how the compiler finds functions
        
5. **C++17 & C++20 Additions**
    
    - Structured bindings, if/switch init statements, `std::string_view`, coroutines (C++20), ranges library (C++20) (depending on job context)
        
6. **Low-level & ABI**
    
    - If your role is more system-level: alignment, object layout, name mangling, calling conventions
        

---

## 9. Build Systems & Tooling

1. **Compilers & Flags**
    
    - Clang, GCC, MSVC basics, warnings, optimization levels
        
2. **Build Systems**
    
    - CMake, Make, Ninja, etc.
        
3. **Debugging Tools**
    
    - GDB, LLDB, Visual Studio Debugger
        
4. **Profiling & Sanitizers**
    
    - AddressSanitizer, LeakSanitizer, Valgrind, perf, etc.
        

**Why:** Practical C++ jobs require you to build, debug, and profile code effectively.

---

## 10. Common Data Structures & Algorithms (Interview-Focused)

1. **Arrays, Linked Lists**
    
    - Implementation details, complexity
        
2. **Stacks, Queues, Deques**
    
    - Typical usage, complexity
        
3. **Trees & Graphs**
    
    - Binary search trees, heaps, adjacency lists
        
4. **Sorting & Searching**
    
    - QuickSort, MergeSort, BFS/DFS, binary search
        
5. **Hash Tables**
    
    - Collisions, open addressing vs. chaining
        
6. **Complexity Analysis**
    
    - Big-O notations, memory vs. performance trade-offs
        

**Why:** Interviewers commonly expect you to know core DS&A, which may also be tested in coding challenges.

---

## 11. Testing & Best Practices

1. **Unit Testing**
    
    - Google Test, Catch2, doctest, etc.
        
2. **Defensive Programming**
    
    - Checking preconditions, contract-based design
        
3. **Naming Conventions & Code Style**
    
    - Consistency is vital in large codebases
        
4. **Error Handling**
    
    - Exceptions vs. error codes, RAII for resource safety
        

---

## 12. Code Organization & Larger Patterns

1. **Namespaces**
    
    - Avoid name collisions, logical grouping
        
2. **Header Files**
    
    - Minimizing includes, forward declarations, PIMPL idiom
        
3. **Design Patterns**
    
    - Singleton, Factory, Strategy, Observer, etc. in a C++ context
        

---

## 13. Modern C++ Idioms & Patterns

1. **Resource Acquisition Is Initialization (RAII)**
    
    - Smart pointers, auto-cleanup
        
2. **Rule of Zero/Five**
    
    - If you need a custom destructor, copy, or move, do so carefully
        
3. **Perfect Forwarding & Type Deduction**
    
    - `auto`, `decltype`, `decltype(auto)`, universal references
        
4. **CRTP (Curiously Recurring Template Pattern)**
    
    - For advanced libraries, EBO (empty base optimization)
        

---

## 14. (Optional) Meta & Low-Level Knowledge

1. **Templates & Metaprogramming** (advanced)
    
    - If you aim for library or framework development
        
2. **Assembly & Compiler Intrinsics**
    
    - For performance-critical systems
        
3. **ABI compatibility, name mangling**
    
    - Important for distributed library development
        

---

## Conclusion

This roadmap should help guide your learning for modern, professional C++ development. **Interview questions** frequently test your knowledge of:

- **Memory management** and **pointer handling**
    
- **Object construction** (copy vs. move)
    
- **Standard library containers** and **algorithms**
    
- **Templates** (basics, specialization, typical pitfalls)
    
- **Multithreading** (mutex, atomic, concurrency patterns)
    
- **Practical problem-solving** with DS&A knowledge
    

Stay up to date with **latest C++ standards** (C++17, C++20, C++23) for new features. Master these topics, build personal projects, and you’ll be well on your way to being an employable C++ developer.