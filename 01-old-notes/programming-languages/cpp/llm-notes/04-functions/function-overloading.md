# Function Overloading in C++

Function overloading allows multiple functions with the **same name** but **different parameter lists** in the same scope. This makes code more expressive by grouping conceptually similar operations under a single function name.

```cpp
#include <iostream> // For I/O
#include <string> // For std::string
#include <vector> // For std::vector in rvalue reference examples
#include <cstdarg> // For va_list, va_start, va_end in ellipsis examples
```

---

## Overloading Principles

When two or more functions have the **same name** but **different parameter lists**, the compiler decides which to call based on the arguments at the call site.

- Overload **signature** includes:
    
    - Function name.
        
    - Parameter types, order, and count.
        
    - const/volatile qualifiers on member functions (not relevant for free functions).
        
- **Return type** is **not** part of the function signature.
    

```cpp
// Example of basic function overloading
void print(int value) {
    std::cout << "Integer: " << value << '\n';
}

void print(double value) {
    std::cout << "Double: " << value << '\n';
}

void print(const std::string& value) {
    std::cout << "String: " << value << '\n';
}

// Usage
print(42); // calls print(int)
print(3.14); // calls print(double)
print("Hello"); // calls print(const std::string&) (implicit conversion from const char*)
```

---

## Name Mangling

C++ compilers internally generate unique **mangled names** to distinguish overloaded functions with the same name but different parameter types:

```cpp
void process(int x);
void process(double x);

// Mangled names (example, compiler-dependent):
// _Z7processi  -> process(int)
// _Z7processd  -> process(double)
```

- Use tools like `nm -C` (GCC) or `dumpbin /SYMBOLS` (MSVC) to see mangled names.
    
- `extern "C"` disables name mangling for C interoperability but also disallows overloading in C.
    

---

## Overloading Resolution Rules

The compiler applies a set of rules to find the **best match**:

### Exact Match

Exact matches are chosen over conversions.

```cpp
void func(int x) {
    std::cout << "func(int)" << '\n';
}

void func(double x) {
    std::cout << "func(double)" << '\n';
}

int i{42};
func(i); // func(int) - exact match
```

### Promotion

If no exact match, the compiler tries **promotions** (e.g., `char` -> `int`, `float` -> `double`).

```cpp
void display(int x) {
    std::cout << "display(int)" << '\n';
}

char c{'A'};
display(c); // c -> int
```

### Standard Conversion

If promotions don’t resolve it, **standard conversions** are considered (e.g., int -> long, double -> float, etc.).

```cpp
void calculate(double x);
void calculate(long x);

int i{42};
calculate(i); // Possibly calls calculate(long) if int->long is better than int->double
```

### User-defined Conversion

Next level of preference is **user-defined conversions** (constructors or operator conversion functions) if standard conversions do not yield a single best match.

```cpp
class String {
public:
    String(const char* s) : data(s) {}
    operator bool() const { return !data.empty(); }
private:
    std::string data;
};

void evaluate(bool b);
void evaluate(const String& s);

String str{"Hello"};
evaluate(str); // Calls evaluate(const String&)
```

### Ellipsis Match

Overloads with ellipses (`...`) have **lowest priority**.

```cpp
void log(const char* fmt, ...);
void log(const std::string& msg);

log("Value: %d", 42); // calls log(const char*, ...)
```

---

## Ambiguity in Overload Resolution

If the compiler cannot choose a unique best match, it reports an **ambiguous call**.

```cpp
void ambiguous(int x, double y);
void ambiguous(double x, int y);

// ambiguous(10, 10); // error: ambiguous

// Fix with explicit casts
ambiguous(10, 10.0);   // picks (int, double)
ambiguous(10.0, 10);   // picks (double, int)
```

---

## Overloading with References

You can overload functions on **reference types** (lvalue vs rvalue references, const vs non-const, etc.).

```cpp
void process(int& x) {
    std::cout << "process(int&)" << '\n';
}

void process(const int& x) {
    std::cout << "process(const int&)" << '\n';
}

int a{5};
process(a);    // process(int&)
process(42);   // process(const int&) (42 is an rvalue)
```

---

## Overloading with const/volatile

**Member** functions can be overloaded on their const or volatile qualification:

```cpp
class Data {
public:
    void display() {
        std::cout << "Non-const display()" << '\n';
    }
    void display() const {
        std::cout << "Const display()" << '\n';
    }
};

Data d;
d.display(); // non-const version

const Data cd;
cd.display(); // const version
```

---

## Overloading with rvalue References

Rvalue references (`T&&`) enable **move semantics** and can be overloaded alongside lvalue references.

```cpp
void transfer(std::vector<int>& vec) {
    std::cout << "transfer lvalue" << '\n';
}

void transfer(std::vector<int>&& vec) {
    std::cout << "transfer rvalue" << '\n';
    std::vector<int> local{std::move(vec)}; // steal resources
}

std::vector<int> v{1,2,3};
transfer(v);                       // lvalue
transfer(std::vector<int>{4,5,6}); // rvalue
transfer(std::move(v));            // rvalue
```

---

## Overloading on Return Type (Impossible)

C++ **does not** allow overloading solely on return type; parameter lists must differ.

```cpp
int getValue();
// double getValue(); // error

// Instead, consider different function names, or templates:
template <typename T>
T getValue() {
    // ...
}
```

---

## Overloading and Type Aliases

**Type aliases** (`typedef` or `using`) do not create distinct types for overload.

```cpp
typedef int Integer;
using MyInt = int;

void show(int x);
// void show(Integer x); // same as show(int x)
```

---

## Overloading and Default Arguments

Be careful when mixing **default arguments** and overloading:

```cpp
void configure(int value, bool verbose = false);
void configure(int value);

// configure(42); // ambiguous

configure(42, true); // OK
```

Often it’s clearer to use **one** function with a default argument instead of multiple overloads.

---

## Overloading and Function Templates

Templates can coexist with overloaded functions.

```cpp
template<typename T>
void convert(T x) {
    std::cout << "Template convert: " << x << '\n';
}

void convert(int x) {
    std::cout << "Overloaded convert(int): " << x << '\n';
}

convert(3.14); // calls template
convert(42);   // calls convert(int)
```

Rules:

1. Non-template overloads take precedence if exact match.
    
2. Among templates, more specialized templates are preferred.
    
3. If still ambiguous, it’s an error.
    

---

## Address of Overloaded Functions

Taking the address of an overloaded function requires **disambiguation**.

```cpp
void action(int x);
void action(double x);

// void (*fn)() = &action; // error: which one?

void (*intAction)(int) = &action;       // picks action(int)
void (*doubleAction)(double) = &action; // picks action(double)
```

---

## Overloading in Different Namespaces

Functions in different namespaces don’t overload each other, but can create confusion if you use `using namespace`:

```cpp
namespace Graphics {
    void draw(int x, int y);
}

namespace Text {
    void draw(const std::string& text);
}

using namespace Graphics;
using namespace Text;
// draw(10,20);    // calls Graphics::draw
// draw("Hello"); // calls Text::draw
```

If two namespaces each define `calculate(int)`, a call `calculate(10);` can be ambiguous when both are in scope.

---

## Best Practices for Function Overloading

1. **Keep overloads conceptually related:**
    
    ```cpp
    // Good
    int add(int a, int b);
    double add(double a, double b);
    
    // Bad
    void process(Data* data);
    void process(Logger* log); // different semantics
    ```
    
2. **Maintain consistent parameter ordering and meaning:**
    
    ```cpp
    void setPosition(int x, int y);
    void setPosition(int x, int y, int z);
    ```
    
3. **Avoid confusing overloads:**
    
    ```cpp
    void update(int value);
    void update(bool active);
    // update(0) calls update(int)
    ```
    
4. **Prefer default arguments over multiple overloads** if they serve the same purpose.
    
5. **Be mindful of promotions and conversions** that can unexpectedly match.
    
6. **Use deleted functions** to block undesired overloads.
    
7. **For member functions**, provide const versions when appropriate.
    
8. **When many overloads get unwieldy**, consider alternatives (e.g., a single function with a config struct, or a template for multiple types).
    
9. **Explicit naming** can be clearer than overloading if the semantics differ significantly.
    

---

**In summary**, function overloading is a powerful feature to make code clearer and more expressive. Understanding the rules of overload resolution, potential pitfalls, and best practices will help you use overloading effectively without creating ambiguity or confusion.