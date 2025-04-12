# Fundamental Types and Type Conversions in C++

This note covers the core fundamental data types in C++, including their sizes, value limits, initialization styles, and type conversions.

---

## Overview of Fundamental Types

C++ provides several built-in types, grouped broadly into:

- **Integral types** (for whole numbers)
    
- **Fixed-width integer types** (defined in `<cstdint>`)
    
- **Floating-point types** (for decimal numbers)
    
- **Boolean type**
    
- **Character type**
    
- **Void type**
    

---

## Integral Types

### Signed Integer Types (from `<limits>`)

|Type|Size (bytes)|Minimum Value|Maximum Value|
|---|---|---|---|
|`short`|2|-32,768|32,767|
|`int`|4|-2,147,483,648|2,147,483,647|
|`long`|4 or 8|Platform-dependent|Platform-dependent|
|`long long`|8|-9,223,372,036,854,775,808|9,223,372,036,854,775,807|

### Unsigned Integer Types

|Type|Size (bytes)|Minimum Value|Maximum Value|
|---|---|---|---|
|`unsigned short`|2|0|65,535|
|`unsigned int`|4|0|4,294,967,295|
|`unsigned long`|4 or 8|0|Platform-dependent|
|`unsigned long long`|8|0|18,446,744,073,709,551,615|

### Fixed-Width Integer Types (from `<cstdint>`)

|Type|Size (bits)|Signed Range|Unsigned Range|
|---|---|---|---|
|`int8_t`|8|-128 to 127|—|
|`uint8_t`|8|—|0 to 255|
|`int16_t`|16|-32,768 to 32,767|—|
|`uint16_t`|16|—|0 to 65,535|
|`int32_t`|32|-2,147,483,648 to 2,147,483,647|—|
|`uint32_t`|32|—|0 to 4,294,967,295|
|`int64_t`|64|-9.2e18 to 9.2e18 (approx.)|—|
|`uint64_t`|64|—|0 to 1.8e19 (approx.)|

#### Interview Question: Fixed-width vs Standard Types

**Q: When should you use fixed-width integer types over standard types?** **A:** Use fixed-width types when you need guaranteed size across platforms (e.g., binary file formats, network protocols, hardware interfaces). Use standard types when you want the compiler to choose the most efficient type for the platform.

```cpp
#include <cstdint> // For fixed-width types
#include <limits> // For std::numeric_limits
```

```cpp
short s{-32768};
int i{42};
long l{1'000'000L};
long long ll{9'223'372'036'854'775'807LL};

unsigned short us{65535};
unsigned int ui{100u};
unsigned long ul{1'000'000UL};
unsigned long long ull{18'446'744'073'709'551'615ULL};

int8_t a8{-128};
uint8_t b8{255};
int16_t a16{-32768};
uint16_t b16{65535};
int32_t a32{-2'147'483'648};
uint32_t b32{4'294'967'295U};
int64_t a64{-9'223'372'036'854'775'808LL};
uint64_t b64{18'446'744'073'709'551'615ULL};
```

### Integer Literals

|Literal|Description|Example|
|---|---|---|
|Decimal|Base 10 (default)|`42`|
|Octal|Base 8 (prefix with `0`)|`052` (equals 42 decimal)|
|Hexadecimal|Base 16 (prefix with `0x` or `0X`)|`0x2A` (equals 42 decimal)|
|Binary (C++14)|Base 2 (prefix with `0b` or `0B`)|`0b101010` (equals 42 decimal)|

### Integer Suffixes

|Suffix|Meaning|Example|
|---|---|---|
|`u` or `U`|unsigned|`42U`|
|`l` or `L`|long|`42L`|
|`ll` or `LL`|long long|`42LL`|
|`ul` or `UL`|unsigned long|`42UL`|
|`ull` or `ULL`|unsigned long long|`42ULL`|

---

## Floating-Point Types

|Type|Size (bytes)|Precision|Approximate Range|
|---|---|---|---|
|`float`|4|~7 digits|±1.5e-45 to ±3.4e+38|
|`double`|8|~15-16 digits|±5.0e-324 to ±1.7e+308|
|`long double`|>=8|Varies by compiler|Implementation-defined|

### Special Floating-Point Values

|Value|Description|Access|
|---|---|---|
|Infinity|Positive/negative infinity|`std::numeric_limits<double>::infinity()`|
|NaN|Not a Number (undefined/invalid)|`std::numeric_limits<double>::quiet_NaN()`|
|Denormal|Numbers with reduced precision|`std::numeric_limits<double>::denorm_min()`|

### Floating-Point Literals

```cpp
float f{0.75f};           // f or F suffix for float
double d{3.14159};        // No suffix needed for double
double d2{3.14159e0};     // Scientific notation
long double ld{2.7182L};  // l or L suffix for long double
```

#### Interview Question: Floating-Point Precision

**Q: Why might `0.1 + 0.2 != 0.3` in C++?** **A:** Floating-point numbers are stored in binary format, but decimal fractions like 0.1 and 0.2 cannot be represented exactly in binary. This leads to small rounding errors which accumulate in calculations. For money and exact decimal calculations, use fixed-point arithmetic or libraries like `<decimal>`.

---

## Boolean Type

```cpp
bool is_ready{true};
bool is_empty{false};
```

Used in conditional logic and flow control.

#### Interview Question: Boolean Conversion

**Q: What is the result of the following code and why?**

```cpp
int i = 42;
bool b = i;
int j = b;
```

**A:** `b` will be `true` because any non-zero integer converts to `true` in a boolean context. `j` will be `1` because `true` converts to `1` when a boolean is converted to an integer.

---

## Character Type

|Type|Size|Description|Example|
|---|---|---|---|
|`char`|1 byte|Basic character type|`'A'`|
|`wchar_t`|Platform-specific|Wide character type|`L'Ω'`|
|`char16_t`|2 bytes|UTF-16 character type (C++11)|`u'A'`|
|`char32_t`|4 bytes|UTF-32 character type (C++11)|`U'A'`|
|`char8_t`|1 byte|UTF-8 character type (C++20)|`u8'A'`|

```cpp
char c{'A'};
char newline{'\n'};

char16_t u16{u'\u0041'}; // Unicode 16-bit
char32_t u32{U'\U00000041'}; // Unicode 32-bit
wchar_t wc{L'Ω'}; // Wide character
```

### Character Escape Sequences

|Escape Sequence|Meaning|
|---|---|
|`\n`|Newline|
|`\t`|Tab|
|`\r`|Carriage return|
|`\\`|Backslash|
|`\'`|Single quote|
|`\"`|Double quote|
|`\0`|Null character|
|`\xhh`|Hexadecimal value (hh)|
|`\ooo`|Octal value (ooo)|

---

## `void` Type

The `void` type has no values and cannot be instantiated. It's used to:

- Indicate functions that return nothing: `void func()`
- Create generic pointers: `void* ptr`

#### Interview Question: void* Usage

**Q: What are the advantages and disadvantages of using `void*` pointers?** **A:**

- **Advantages**: Type-agnostic generic programming, interfacing with C libraries
- **Disadvantages**: No type safety, requires explicit casting, no pointer arithmetic, no member access

---

## `auto` Type Deduction

```cpp
auto value{42}; // int
auto pi{3.14159}; // double
auto flag{true}; // bool
auto name{'Z'}; // char
auto big_number{1LL}; // long long
auto small_number{int8_t{-5}}; // int8_t
```

### Type Deduction Rules

|Initializer|Deduced Type|
|---|---|
|`auto x = 42;`|`int`|
|`auto x = 42u;`|`unsigned int`|
|`auto x = 42.0;`|`double`|
|`auto x = 42.0f;`|`float`|
|`auto x = "hello";`|`const char*`|
|`auto& x = someInt;`|Reference to the type of `someInt`|
|`const auto& x = someInt;`|Const reference to the type of `someInt`|
|`auto&& x = someValue;`|Universal reference (forwarding reference)|

#### Interview Question: auto Keyword

**Q: What are the benefits and potential pitfalls of using the `auto` keyword?** **A:**

- **Benefits**: Reduces verbosity, avoids type mismatches, adapts to changes in return types
- **Pitfalls**: Can hide intended types making code harder to read, may lead to unexpected behaviors (especially with proxy objects like `vector<bool>::reference`)

Use `auto` for readability when the type is obvious or overly verbose.

---

## Constants

### `const` and `constexpr`

```cpp
const int id{100}; // Cannot be modified at runtime
constexpr double pi{3.14159}; // Must be known at compile time
```

### `constinit` (C++20)

```cpp
constinit static int value = 42; // Guarantees initialization at compile time
```

### `consteval` (C++20)

```cpp
consteval int square(int n) { return n * n; } // Always evaluated at compile time
```

#### Interview Question: const vs constexpr

**Q: What is the difference between `const` and `constexpr`?** **A:**

- `const` indicates a value cannot be modified after initialization
- `constexpr` indicates the value is known at compile time and can be used in contexts requiring compile-time constants
- `const` values may be determined at runtime, while `constexpr` values must be determined at compile time
- Both `const` and `constexpr` functions can be called at runtime, but only `constexpr` functions can be called in compile-time contexts

Use `const` for values that don't change. Use `constexpr` for compile-time constants.

---

## Type Conversions

### Implicit Conversions

```cpp
int a{10};
double b{a}; // int to double (safe)
int c{3.7}; // double to int (narrowing, truncates)
```

### Conversion Ranks

Integral promotion order:

1. `bool`
2. `char`, `signed char`, `unsigned char`, `short`, `unsigned short`
3. `int`, `unsigned int`
4. `long`, `unsigned long`
5. `long long`, `unsigned long long`

Floating-point promotion order:

1. `float`
2. `double`
3. `long double`

### Explicit Casts

```cpp
// C-style cast (avoid)
double d1 = 3.99;
int i1 = (int)d1; // Truncates to 3

// C++ style casts
double d2 = 3.99;
int i2 = static_cast<int>(d2); // Truncates to 3

const int c = 42;
int* p = const_cast<int*>(&c); // Removes const (dangerous)

Base* b = new Derived();
Derived* d = dynamic_cast<Derived*>(b); // Safe downcasting with runtime check

struct S { int x; } s;
int* px = reinterpret_cast<int*>(&s); // Low-level reinterpretation of bit pattern
```

#### Interview Question: Type Cast Operators

**Q: Explain the difference between C++'s four cast operators and when you would use each one.** **A:**

- `static_cast`: General-purpose casting for well-defined conversions. Use for numeric conversions and upcasting in inheritance hierarchies.
- `dynamic_cast`: Safe downcasting in inheritance hierarchies with runtime type checking. Returns nullptr for pointers or throws for references if cast fails. Requires polymorphic types.
- `const_cast`: Only removes const/volatile qualifiers. Use sparingly when interfacing with APIs that aren't const-correct.
- `reinterpret_cast`: Low-level reinterpretation of bit patterns. Use for pointer-to-integer conversions or other platform-specific, non-portable operations.

### Compile-Time Conversions

```cpp
constexpr double exact{2.718};
constexpr int truncated{static_cast<int>(exact)};
```

### User-Defined Conversions

```cpp
class Fraction {
private:
    int numerator;
    int denominator;
public:
    Fraction(int n, int d = 1) : numerator(n), denominator(d) {}
    
    // Implicit conversion operator
    operator double() const { return static_cast<double>(numerator) / denominator; }
    
    // Explicit conversion operator
    explicit operator bool() const { return numerator != 0; }
};

Fraction f(3, 4);
double d = f;        // Implicit conversion to 0.75
bool b = static_cast<bool>(f);  // Explicit conversion needed
```

---

## Type Traits (C++11, `<type_traits>`)

```cpp
#include <type_traits>

// Check if a type is integral
static_assert(std::is_integral<int>::value, "int must be integral");

// Check if types are the same
static_assert(std::is_same<int, int32_t>::value, "int must be 32 bits");

// Remove const qualification
using nonconst_type = std::remove_const<const int>::type; // int

// Enable function only for numeric types
template <typename T>
std::enable_if_t<std::is_arithmetic<T>::value, T> 
square(T value) { return value * value; }
```

#### Interview Question: Type Traits

**Q: How can type traits help with template metaprogramming?** **A:** Type traits enable compile-time introspection and type manipulation, allowing for:

- Compile-time condition checks with `static_assert`
- Conditional template specialization using SFINAE or `if constexpr`
- Type transformations like `remove_reference` or `add_const`
- SFINAE-based function overloading with `enable_if`
- Optimizations based on type properties

---

## Initialization Methods

|Method|Example|Notes|
|---|---|---|
|Default|`int a;`|Uninitialized (indeterminate) for local variables|
|Copy|`int a = 42;`|Traditional C-style|
|Direct|`int a(42);`|Function-style|
|List (C++11)|`int a{42};`|Prevents narrowing conversions|
|List with =|`int a = {42};`|Combines copy and list initialization|

```cpp
int a;           // Default: indeterminate value
int b = 42;      // Copy initialization
int c(42);       // Direct initialization
int d{42};       // List initialization (preferred in modern C++)
int e = {42};    // Copy list initialization
```

### Uniform Initialization vs. Narrowing Conversion

```cpp
int x1 = 3.14;   // Allowed: narrowing conversion from double to int
// int x2{3.14}; // Error: narrowing conversion not allowed in list initialization
```

#### Interview Question: C++11 Initialization

**Q: Why is list initialization (`{}`) generally preferred in modern C++?** **A:** List initialization offers several advantages:

- Prevents narrowing conversions at compile time (int to smaller int, float to int)
- Works consistently across all types (primitives, arrays, objects, etc.)
- Can initialize aggregate types (arrays and structs) directly
- Avoids the most vexing parse problem (where the compiler misinterprets a constructor call as a function declaration)

---

## Best Practices

- Prefer `int` and `double` unless specific size/precision needed
    
- Use `std::intN_t` and `std::uintN_t` for portable fixed-width types
    
- Use `auto` to reduce verbosity where appropriate
    
- Use `const` or `constexpr` for immutability and safety
    
- Avoid mixing signed and unsigned types
    
- Always prefer `static_cast` over C-style casts
    
- Use brace initialization `{}` to prevent narrowing conversions
    
- Use `std::size_t` for sizes and indices (not `int`)
    
- Consider memory alignment when working with low-level data structures
    

---

## Common Technical Interview Questions

1. **Q:** What happens when you assign a negative value to an unsigned type?  
    **A:** The negative value is converted to its two's complement representation, resulting in a large positive value. For example: `uint8_t x = -1;` assigns 255 to x.
    
2. **Q:** What is the difference between `char`, `signed char`, and `unsigned char`?  
    **A:** `char` can be either signed or unsigned depending on the implementation. `signed char` and `unsigned char` have explicit signedness. All three have the same size but potentially different ranges.
    
3. **Q:** How do you detect integer overflow in C++?  
    **A:** C++ doesn't automatically detect integer overflow for built-in types. Solutions include:
    
    - Using `if` statements to check before operations
    - Using safe math libraries
    - Using the `<limits>` header to check boundary conditions
    - Using compiler-specific intrinsics/built-ins
4. **Q:** What is a trivially copyable type?  
    **A:** A type that can be safely copied byte-by-byte with `memcpy()`. It has no virtual functions, virtual base classes, or non-trivial copy/move semantics. Check with `std::is_trivially_copyable`.
    
5. **Q:** Explain the alignment requirements of different types. Why does it matter?  
    **A:** Alignment refers to memory address restrictions for data types. For example, `int` may need to be at addresses divisible by 4. Proper alignment:
    
    - Improves performance (misaligned access is slower or can cause exceptions)
    - Is required for certain hardware/instructions
    - Affects structure size due to padding

---

## Summary

Understanding C++'s type system and conversions is essential for correctness and performance. Mastery of these basics builds the foundation for all higher-level C++ programming tasks. The type system in C++ is comprehensive but complex, providing both safety and flexibility when used correctly.