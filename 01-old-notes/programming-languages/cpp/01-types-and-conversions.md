# Types & Conversions

## 1  Fundamental Built‑in Types

> _Use these snippets to copy‑paste into Compiler Explorer or `main.cpp` as you read._


### Boolean

**`bool`**

```cpp
bool is_ready = false;
```


### Integral

**`char` / `signed char` / `unsigned char`**

```cpp
char letter = 'A';
unsigned char bits = 0xFF;   // 255
```

**`char8_t` (C++20)**

```cpp
char8_t euro = u8'€';
```

**`char16_t` / `char32_t` / `wchar_t`**

```cpp
char16_t heart = u"\u2665"[0];
wchar_t wide = L'Ж';
```

**`short` / `unsigned short`**

```cpp
short temperature = -5;
unsigned short port = 8080;
```

**`int` / `unsigned int`**

```cpp
int answer = 42;
unsigned int mask = 0b1111'0000;
```

**`long` / `unsigned long`**

```cpp
long population = 8'000'000L;
```

**`long long` / `unsigned long long`**

```cpp
unsigned long long max64 = 18'446'744'073'709'551'615ULL;
```

### 1.2 Floating‑Point

**`float`**

```cpp
float ratio = 3.5f;
```

**`double`**

```cpp
double pi = 3.141592653589793;
```

**`long double`**

```cpp
long double high_prec = 3.141592653589793238462643383279L;
```

### 1.3 Fixed‑Width Aliases `<cstdint>` 🟢

**`std::int8_t` / `std::uint8_t`**

```cpp
std::int8_t delta = -128;
std::uint8_t mask8 = 0xFF;
```

**`std::int16_t` / `std::uint16_t`**

```cpp
std::int16_t audioSample = -32'768;
std::uint16_t port = 65535;
```

**`std::int32_t` / `std::uint32_t`**

```cpp
std::int32_t counter = 1'000'000;
std::uint32_t rgba = 0xFF'AA'00'FFu;
```

**`std::int64_t` / `std::uint64_t`**

```cpp
std::int64_t offset = -9'000'000'000LL;
std::uint64_t big = 18'446'744'073'709'551'615ULL;
```

**`std::intptr_t` / `std::uintptr_t`**

```cpp
int value = 5;
std::uintptr_t address = reinterpret_cast<std::uintptr_t>(&value);
```

**`std::size_t` / `std::ptrdiff_t`**

```cpp
std::size_t len = sizeof(address);
std::ptrdiff_t diff = reinterpret_cast<char*>(&value + 1) - reinterpret_cast<char*>(&value);
```

> **Tip 🔵** Prefer fixed‑width types for portable binary interfaces and to make intent explicit.

---

## 2  Size & Range Cheat‑Sheet

_LP64, two’s‑complement x86‑64 GCC/Clang; **always** confirm with `sizeof` / `std::numeric_limits<>` on your target platform._

|Type|`sizeof` (bytes)|Min|Max|
|---|--:|--:|--:|
|`bool`|1|0|1|
|`char`†|1|−128|127|
|`unsigned char`|1|0|255|
|`char8_t`|1|0|255|
|`wchar_t`|4 (Linux) / 2 (Win)|0|implementation‑def|
|`short`|2|−32 768|32 767|
|`unsigned short`|2|0|65 535|
|`int`|4|−2 147 483 648|2 147 483 647|
|`unsigned int`|4|0|4 294 967 295|
|`long`|8|−9 223 372 036 854 775 808|9 223 372 036 854 775 807|
|`unsigned long`|8|0|18 446 744 073 709 551 615|
|`long long`|8|same as `long` on LP64||
|`float`|4|~1.4 × 10⁻⁴⁵|~3.4 × 10³⁸|
|`double`|8|~5.0 × 10⁻³²⁴|~1.7 × 10³⁰⁸|
|`long double`|16|system‑specific||

† Signedness of plain `char` is implementation‑defined.

```cpp
#include <limits>
#include <iostream>
std::cout << std::numeric_limits<int>::max(); // 2147483647
```

---

## 3  cv‑Qualifiers & Storage Duration (with Tiny Snippets)

- **`const`** — read‑only after initialization; enables compile‑time propagation.
    
    ```cpp
    const double tau = 6.283185307179586;
    ```
    
- **`volatile`** — tells the compiler the value can change outside program control.
    
    ```cpp
    volatile std::uint32_t* status = reinterpret_cast<std::uint32_t*>(0x4000'1000);
    ```
    
- **`constexpr`** (C++11) — evaluated at compile time when possible.
    
    ```cpp
    constexpr int cubes(int x) { return x*x*x; }
    static_assert(cubes(3) == 27);
    ```
    
- **`consteval`** (C++20) — _must_ be evaluated at compile time.
    
    ```cpp
    consteval int answer() { return 42; }
    int x = answer();
    ```
    
- **`mutable`** — allows modification inside `const` objects.
    
    ```cpp
    struct Cache { mutable int hits{}; int get() const { return ++hits; } };
    ```
    

---

## 4  Type Deduction Tools

|Tool|Example|Result|
|---|---|---|
|`auto`|`auto n = 1u;`|`unsigned int`|
|`auto&`|`auto& ref = n;`|`unsigned int&`|
|`decltype(expr)`|`decltype(n) m = 0;`|same type as `n`|
|`decltype(auto)`|`decltype(auto) z = (n);`|preserves cv/ref exactly|

> **Gotcha 🟡** Bare `auto` strips top‑level `const`.

---

## 5  Conversions

### 5.1 Implicit – Standard Conversions

```cpp
char c = 'A';
int code = c;                 // integral promotion
float f = code;               // integral‑to‑floating
bool ok = code;               // integral‑to‑bool
```

_Dropping `const` is **not** allowed implicitly:_

```cpp
const int ci = 5;
// int* p = &ci;   // ❌ error
```

### 5.2 Explicit Casts

- Numeric, safe as possible:
    
    ```cpp
    double pi = 3.14159;
    int truncated = static_cast<int>(pi); // 3
    ```
    
- Checked down‑cast:
    
    ```cpp
    Base* b = new Derived;
    if(auto d = dynamic_cast<Derived*>(b)) d->foo();
    ```
    
- Bit‑level copy (C++20):
    
    ```cpp
    std::uint32_t bits = std::bit_cast<std::uint32_t>(pi);
    ```
    

---

## 6  Fixed‑Width & Limits Reference

```cpp
#include <cstdint>
#include <limits>
std::int16_t audio = std::numeric_limits<std::int16_t>::lowest();
```

---

## 7  Variable Initialization Forms

|Form|Syntax|Notes|
|---|---|---|
|**Default**|`int a;`|indeterminate; avoid|
|**Copy**|`int a = 5;`|may narrow|
|**Direct**|`int a(5);`|good; but not usable with aggregates|
|**Brace‑direct**|`int a{5};`|**preferred** – no narrowing|
|**Value**|`int a{};`|zero‑initialize|

_Brace‑direct prevents bugs:_

```cpp
double d = 3.14;
// int i{d}; // ❌ narrowing error
```

---

## 8  Interview Checkpoints 🟡

- Why is integral promotion required before arithmetic?
    
- Explain difference between `const T*`, `T const*`, and `T* const`.
    
- How does `auto` deduce with `{}` vs `()` initializers?
    

---

## 9  Further Reading & Practice

- **cppreference.com** » Fundamental types; Conversions; Type deduction
    
- **C++ Core Guidelines** – SL‑conversions, ES‑auto, CP‑constexpr
    

---

> 🏁 **Next** → `memory-and-raii.md` (constructors, Rule of 0/3/5/6, smart pointers)

---

_Maintainer notes:_ Lines tagged 🟢🔵🟡🔴 to reflect study priority.