# Integer Types in C++

<br>

---

<br>

## Fundamental Integer Types

C++ includes several primary integer types. Their sizes are not strictly defined by the standard but must meet minimum requirements.

Get the min/max integer limits by including the `<limits>` header:

```cpp
#include <limits>
```

<br>

### short

- **Minimum Size:** 16 bits (2 bytes)
- **Typical Range (signed):** -32,768 to 32,767
- **Typical Range (unsigned):** 0 to 65,535

```cpp
short short_min{std::numeric_limits<short>::min()};  
short short_max{std::numeric_limits<short>::max()};
```

```cpp
unsigned short ushort_min{0u};  
unsigned short ushort_max{std::numeric_limits<unsigned short>::max()};
```

<br>

### int

- **Minimum Size:** 16 bits (typically 32 bits on modern systems)
- **Typical Range (signed):** -2,147,483,648 to 2,147,483,647 (when 32 bits)
- **Typical Range (unsigned):** 0 to 4,294,967,295

```cpp
int int_min{std::numeric_limits<int>::min()};  
int int_max{std::numeric_limits<int>::max()};
```

```cpp
unsigned int uint_min{0u};  
unsigned int uint_max{std::numeric_limits<unsigned int>::max()};
```

<br>

### long

- **Minimum Size:** 32 bits
- **Typical Size:** Either 32 bits or 64 bits depending on the platform (commonly 32 bits on Windows and 64 bits on many Unix-like systems)
- **Range:** When 32 bits, same as 32-bit int; when 64 bits, much larger.

```cpp
long long_min{std::numeric_limits<long>::min()};  
long long_max{std::numeric_limits<long>::max()};
```

```cpp
unsigned long ulong_min{0u};  
unsigned long ulong_max{std::numeric_limits<unsigned long>::max()};
```

<br>

### long long

- **Minimum Size:** 64 bits (8 bytes)
- **Typical Range (signed):** -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807
- **Typical Range (unsigned):** 0 to 18,446,744,073,709,551,615

```cpp
long long long_long_min{std::numeric_limits<long long>::min()};  
long long long_long_max{std::numeric_limits<long long>::max()};
```

```cpp
unsigned long long ulong_long_min{0u};  
unsigned long long ulong_long_max{std::numeric_limits<unsigned long long>::max()};
```

<br>

---

<br>

## Comparison Table of Fundamental Types

|Type|Typical Size (bytes)|Minimum Bit Width|Signed Range|Unsigned Range|
|---|---|---|---|---|
|short|2|16 bits|-32,768 to 32,767|0 to 65,535|
|int|4 (commonly)|16 bits (min)|-2,147,483,648 to 2,147,483,647 (if 32 bits)|0 to 4,294,967,295 (if 32 bits)|
|long|4 or 8|32 bits|-2,147,483,648 to 2,147,483,647 (if 32 bits)|0 to 4,294,967,295 (if 32 bits)|
|long long|8|64 bits|-9,223,372,036,854,775,808 to 9,223,372,036,854,775,807|0 to 18,446,744,073,709,551,615|

> **Note:** The exact sizes can vary by implementation. Always refer to your compiler's documentation or use `sizeof()` to check sizes on your system.

<br>

---

<br>

## Fixed-Width Integer Types

To write portable code where the integer size must be exact, C++ offers fixed-width types in the `<cstdint>` header. These types guarantee the number of bits across platforms.

### Common Fixed-Width Types

|Type|Width|Example Signed Range|Example Unsigned Range|
|---|---|---|---|
|int8_t|8|-128 to 127|0 to 255|
|int16_t|16|-32,768 to 32,767|0 to 65,535|
|int32_t|32|-2,147,483,648 to 2,147,483,647|0 to 4,294,967,295|
|int64_t|64|-9,223,372,036,854,775,808 to 9,223,372,036,854,775,807|0 to 18,446,744,073,709,551,615|

- These types are defined if the implementation supports them.
- For each signed type, there is an equivalent unsigned type (e.g., uint8_t, uint16_t, etc.).

<br>

### int8_t / uint8_t

```cpp
int8_t int8_min{std::numeric_limits<int8_t>::min()};  
int8_t int8_max{std::numeric_limits<int8_t>::max()};
```

```cpp
uint8_t uint8_min{0u};  
uint8_t uint8_max{std::numeric_limits<uint8_t>::max()};
```

<br>

### int16_t / uint16_t

```cpp
int16_t int16_min{std::numeric_limits<int16_t>::min()};  
int16_t int16_max{std::numeric_limits<int16_t>::max()};
```

```cpp
uint16_t uint16_min{0u};  
uint16_t uint16_max{std::numeric_limits<uint16_t>::max()};
```

<br>

### int32_t / uint32_t

```cpp
int32_t int32_min{std::numeric_limits<int32_t>::min()};  
int32_t int32_max{std::numeric_limits<int32_t>::max()};
```

```cpp
uint32_t uint32_min{0u};  
uint32_t uint32_max{std::numeric_limits<uint32_t>::max()};
```

<br>

### int64_t / uint64_t

```cpp
int64_t int64_min{std::numeric_limits<int64_t>::min()};  
int64_t int64_max{std::numeric_limits<int64_t>::max()};
```

```cpp
uint64_t uint64_min{0u};  
uint64_t uint64_max{std::numeric_limits<uint64_t>::max()};
```

<br>

---

<br>

## Size, Range, and Portability Considerations

<br>

### Size and Range

- **Minimum Requirements:**
    - The C++ standard sets minimum limits (e.g., an `int` must be at least 16 bits), but most modern systems use 32 bits for `int`.
    - `short` is generally 16 bits, `int` is 32 bits, and `long long` is 64 bits.
- **Platform Variations:**
    - Some systems might define `long` as 32 bits (e.g., Windows) or 64 bits (e.g., many Unix-like systems).
    - Always verify using `sizeof()` in your code if exact sizes are critical.

<br>

#### Size of Default Integer Types

```cpp
std::cout << "Size of short: " << sizeof(short) << " bytes\n";  
std::cout << "Size of unsigned short: " << sizeof(unsigned short) << " bytes\n";  
  
std::cout << "Size of int: " << sizeof(int) << " bytes\n";  
std::cout << "Size of unsigned int: " << sizeof(unsigned int) << " bytes\n";  
  
std::cout << "Size of long: " << sizeof(long) << " bytes\n";  
std::cout << "Size of unsigned long: " << sizeof(unsigned long) << " bytes\n";  
  
std::cout << "Size of long long: " << sizeof(long long) << " bytes\n";  
std::cout << "Size of unsigned long long: " << sizeof(unsigned long long) << " bytes\n";
```

<br>

#### Size of Fixed-Size Integer Types

```cpp
std::cout << "Size of int8_t: " << sizeof(int8_t) << " bytes\n";
std::cout << "Size of uint8_t: " << sizeof(uint8_t) << " bytes\n";

std::cout << "Size of int16_t: " << sizeof(int16_t) << " bytes\n";
std::cout << "Size of uint16_t: " << sizeof(uint16_t) << " bytes\n";

std::cout << "Size of int32_t: " << sizeof(int32_t) << " bytes\n";
std::cout << "Size of uint32_t: " << sizeof(uint32_t) << " bytes\n";

std::cout << "Size of int64_t: " << sizeof(int64_t) << " bytes\n";
std::cout << "Size of uint64_t: " << sizeof(uint64_t) << " bytes\n";
```

<br>

### Portability Tips

- **Use Fixed-Width Types When Necessary:**  
    If your application depends on exact sizes (e.g., file formats, network protocols), use types from `<cstdint>`.
    
- **Be Cautious with Assumptions:**  
    Do not assume that `int` and `long` have the same size across different platforms.
    
- **Utilize Compiler Macros and Features:**  
    Many compilers offer macros that reveal information about integer sizes (e.g., `INT_MAX`, `LONG_MAX` from `<climits>`).
    
- **Testing on Multiple Platforms:**  
    When developing portable code, test your application on different architectures to ensure the behavior of integer types is consistent.
    
