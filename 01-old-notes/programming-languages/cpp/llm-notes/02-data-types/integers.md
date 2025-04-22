# Integer Types in C++

C++ provides a variety of integer types to handle different ranges of whole numbers. Understanding these types is essential for efficient memory usage, preventing overflow errors, and ensuring portability across different platforms.

```cpp
#include <iostream> // Input/output stream operations: cin, cout, cerr, etc.
#include <limits> // Numeric limits information: min/max values for data types
#include <cstdint> // Fixed-width integer types: int8_t, uint32_t, etc.
#include <vector> // Dynamic array container: std::vector
#include <string> // String handling: std::string
```

## Basic Integer Types

C++ includes several fundamental integer types with implementation-defined sizes.

### short

The `short` (or `short int`) type is used for small integer values when memory conservation is important.

```cpp
short yearOffset{20}; // Relative year (e.g., years since 2000)
short temperature{-15}; // Temperature in Celsius
short elevationChange{1250}; // Height change in meters

// Size and range info
std::cout << "short size: " << sizeof(short) << " bytes\n";
std::cout << "short min value: " << std::numeric_limits<short>::min() << '\n';
std::cout << "short max value: " << std::numeric_limits<short>::max() << '\n';
```

#### Size and Range

- **Size**: At least 2 bytes (typically 2 bytes on most platforms)
- **Range**: At least -32,768 to 32,767 (-2^15 to 2^15 - 1)
- **Common uses**: Small ranges like days in a month, hours, temperature values

### int

The `int` type is the most commonly used integer type, balancing range and performance.

```cpp
int userCount{10485}; // Number of users
int fileSize{1048576}; // File size in bytes
int colorCode{0x00FF00}; // RGB color code (green)

// Loop counter - common use case for int
for (int i = 0; i < 10; ++i) {
    // Process items
}

// Integer arithmetic
int totalBytes{fileSize * 3};
```

#### Size and Range

- **Size**: At least 2 bytes (typically 4 bytes on most modern platforms)
- **Range**: At least -32,768 to 32,767, usually -2,147,483,648 to 2,147,483,647 for 4-byte implementations
- **Common uses**: Loop counters, medium-sized counts, status codes, everyday calculations

### long

The `long` (or `long int`) type provides a potentially larger range than `int`.

```cpp
long populationCount{8000000000L}; // World population estimate with 'L' suffix
long filePosition{1073741824L}; // Position in a large file (1 GB)

// Timestamp in seconds since epoch (common use case for long)
long currentTime{static_cast<long>(std::chrono::system_clock::to_time_t(
                std::chrono::system_clock::now()))};
```

#### Size and Range

- **Size**: At least 4 bytes
  - 4 bytes on most 32-bit and 64-bit Windows
  - 8 bytes on most 64-bit Unix/Linux systems
- **Range**:
  - At least -2,147,483,648 to 2,147,483,647
  - On 8-byte implementations: -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807
- **Common uses**: Timestamps, file positions, system resource IDs

### long long

The `long long` (or `long long int`) type, introduced in C++11, provides the largest standard integer type.

```cpp
long long worldPopulation{7'950'000'000LL}; // Global population with 'LL' suffix
long long bytesTransferred{2'500'000'000'000LL}; // Network traffic in bytes
long long distanceToStar{9'460'800'000'000'000LL}; // Distance in meters

// Large-scale calculations
long long dataProcessingCapacity{1'000'000LL * 1'000'000LL}; // Operations per second
```

#### Size and Range

- **Size**: At least 8 bytes (64 bits)
- **Range**: -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 (-2^63 to 2^63 - 1)
- **Common uses**: Very large counts, scientific calculations, high-precision timestamps

### Unsigned Variants

Each basic integer type has an unsigned variant that doubles the positive range by eliminating negative values.

```cpp
unsigned short pixelValue{65000}; // 16-bit color value
unsigned int ipAddress{0xC0A80001u}; // IP address (192.168.0.1) with 'u' suffix
unsigned long fileSize{4'294'967'295UL}; // File size in bytes with 'UL' suffix
unsigned long long memoryAddress{0xFFFFF000ULL}; // Memory address with 'ULL' suffix

// Bit manipulation (common with unsigned types)
unsigned int flags{0};
flags |= (1u << 3); // Set bit 3
flags |= (1u << 5); // Set bit 5
```

#### Unsigned Ranges

| Type                 | Typical Size | Range                                                 | Common Uses                                |
| -------------------- | ------------ | ----------------------------------------------------- | ------------------------------------------ |
| `unsigned short`     | 2 bytes      | 0 to 65,535                                           | Color values, small ports, character codes |
| `unsigned int`       | 4 bytes      | 0 to 4,294,967,295                                    | Array indices, status flags, RGB colors    |
| `unsigned long`      | 4-8 bytes    | 0 to 4,294,967,295 or 0 to 18,446,744,073,709,551,615 | File sizes, memory sizes                   |
| `unsigned long long` | 8 bytes      | 0 to 18,446,744,073,709,551,615                       | Very large counts, unique IDs              |

## Fixed-Width Integer Types (C++11)

The `<cstdint>` header provides integer types with guaranteed sizes, addressing the portability issues of basic integer types.

### Exact-Width Integer Types

These types guarantee a specific number of bits.

```cpp
// Used for exact control over data sizes
int8_t temperature{24}; // Temperature value fitting in a byte
int16_t audioSample{-16384}; // Audio sample in 16-bit PCM format
int32_t pixelColor{0x00FFFFFF}; // RGB color with alpha channel
int64_t filePosition{1'152'921'504LL}; // Position in a very large file

// Common in networking and binary protocols
uint8_t headerFlag{0x7F}; // Protocol header flag
uint16_t networkPort{8080}; // Network port number
uint32_t ipAddress{0xC0A80001}; // IPv4 address (192.168.0.1)
uint64_t deviceId{0x123456789ABCDEF0ULL}; // Unique device identifier

// Binary file handling
std::cout << "Writing " << sizeof(uint32_t) << " bytes for ID\n";
```

#### Size and Range

| Type       | Size    | Range                                                   | Common Uses                            |
| ---------- | ------- | ------------------------------------------------------- | -------------------------------------- |
| `int8_t`   | 1 byte  | -128 to 127                                             | Small sensor values, characters        |
| `uint8_t`  | 1 byte  | 0 to 255                                                | Bytes in binary data, color components |
| `int16_t`  | 2 bytes | -32,768 to 32,767                                       | Audio samples, small measurements      |
| `uint16_t` | 2 bytes | 0 to 65,535                                             | Unicode points, network ports          |
| `int32_t`  | 4 bytes | -2,147,483,648 to 2,147,483,647                         | Coordinates, timestamps                |
| `uint32_t` | 4 bytes | 0 to 4,294,967,295                                      | IPv4 addresses, RGBA colors            |
| `int64_t`  | 8 bytes | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 | High-precision timestamps              |
| `uint64_t` | 8 bytes | 0 to 18,446,744,073,709,551,615                         | File sizes, unique identifiers         |

### Fast and Least Types

The `<cstdint>` header also provides types that focus on either performance or minimum size requirements.

#### Fast Types

Designed for the fastest type that's at least the specified number of bits.

```cpp
// Used in performance-critical code
int_fast8_t loopCounter{0};
int_fast16_t frameRate{60};
int_fast32_t iterationCount{1'000'000};
int_fast64_t computationResult{0};

// Performance-sensitive loop
for (int_fast32_t i = 0; i < iterationCount; ++i) {
    computationResult += i;
}

// Size info (may be larger than the minimum bits)
std::cout << "int_fast16_t size: " << sizeof(int_fast16_t) << " bytes\n";
std::cout << "int_fast32_t size: " << sizeof(int_fast32_t) << " bytes\n";
```

#### Least Types

Designed for the smallest type that's at least the specified number of bits.

```cpp
// Used when memory efficiency is important
struct CompactData {
    int_least8_t status; // Status code (-128 to 127 is sufficient)
    int_least16_t value; // Value with modest range needs
    uint_least8_t flags; // 8 boolean flags packed in a byte
};

// Example: IoT sensor data with memory constraints
CompactData sensorRecord;
sensorRecord.status = 1; // Active status
sensorRecord.value = 1275; // Sensor reading
sensorRecord.flags = 0x5; // Bit flags 0 and 2 set

// Size info (guaranteed minimum size, might be larger)
std::cout << "CompactData size: " << sizeof(CompactData) << " bytes\n";
```

## Special Integer Types

C++ provides several special-purpose integer types for specific use cases.

### size_t

A platform-specific unsigned integer type that represents the maximum size any object can be in memory.

```cpp
// Container sizes and indices
std::vector<int> numbers{10, 20, 30, 40, 50};
std::string text{"Example text"};

size_t vectorSize{numbers.size()};  // Number of elements
size_t stringLength{text.length()}; // String length

// Array indexing
for (size_t i = 0; i < numbers.size(); ++i) {
    // Access elements using i
}

// Memory operations
int* buffer = new int[1000];
size_t bufferSize{1000 * sizeof(int)};
delete[] buffer;
```

#### Size and Range

- **Size**: Depends on platform (4 bytes on 32-bit systems, 8 bytes on 64-bit systems)
- **Range**: 0 to platform-dependent maximum (typically 0 to 4,294,967,295 on 32-bit or 0 to 18,446,744,073,709,551,615 on 64-bit)
- **Use cases**: Array indices, container sizes, memory allocation sizes, loop counters

### ptrdiff_t

A platform-specific signed integer type that represents the difference between two pointers.

```cpp
// Array traversal with pointers
int data[100]{};
for (int i = 0; i < 100; ++i) {
    data[i] = i * 10;
}

int* begin{&data[0]};
int* end{&data[99]};
int* current{begin + 50}; // Pointing to middle element

ptrdiff_t elementsAhead{end - current};
ptrdiff_t elementsBehind{current - begin};

// Iterator differences in STL containers
std::vector<double> values(1000, 0.5);
auto startIter = values.begin();
auto midIter = startIter + 500;

ptrdiff_t distance{midIter - startIter};
```

#### Size and Range

- **Size**: Depends on platform (4 bytes on 32-bit systems, 8 bytes on 64-bit systems)
- **Range**: Platform-dependent (typically -2,147,483,648 to 2,147,483,647 on 32-bit or -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 on 64-bit)
- **Use cases**: Pointer arithmetic, difference between iterators, offsets in arrays

### intmax_t and uintmax_t

The largest supported signed and unsigned integer types.

```cpp
// For calculations requiring maximum integer capacity
intmax_t largeSignedValue{std::numeric_limits<intmax_t>::max() / 2};
uintmax_t largeUnsignedValue{std::numeric_limits<uintmax_t>::max() / 2};

// Example: Factorial calculation requiring very large integers
uintmax_t factorial(unsigned int n) {
    uintmax_t result{1};
    for (unsigned int i = 2; i <= n; ++i) {
        result *= i;
    }
    return result;
}

// Usage
uintmax_t result = factorial(20); // 20! is a very large number
```

#### Size and Range

- **Size**: Typically 8 bytes on modern systems
- **Range**: The largest range supported by the implementation
- **Use cases**: Extremely large integer calculations, maximum possible integer storage

## Implementation Limits

C++ guarantees minimum ranges for integer types, but the actual ranges depend on the implementation.

### Checking Implementation Limits

The `<limits>` header provides information about the limits of numeric types on the current platform.

```cpp
// Getting implementation-specific limits
int minInt = std::numeric_limits<int>::min();
int maxInt = std::numeric_limits<int>::max();

// Check if a type is signed
bool isSigned = std::numeric_limits<char>::is_signed;

// Integer division characteristics
bool isModuloArithmetic = std::numeric_limits<int>::is_modulo;

// Compact display of type ranges
std::cout << "short: "
          << std::numeric_limits<short>::min() << " to "
          << std::numeric_limits<short>::max() << '\n';
```

### Standard Guaranteed Minimum Ranges

C++ standard guarantees these minimum ranges for integer types:

| Type        | Minimum Range                                           |
| ----------- | ------------------------------------------------------- |
| `short`     | -32,767 to 32,767                                       |
| `int`       | -32,767 to 32,767                                       |
| `long`      | -2,147,483,647 to 2,147,483,647                         |
| `long long` | -9,223,372,036,854,775,807 to 9,223,372,036,854,775,807 |

## Integer Literals

C++ provides different suffixes to specify the type of integer literals:

```cpp
// Default integer literals
auto defaultInt = 42; // int

// Typed integer literals
auto unsignedInt = 42u; // unsigned int (u or U suffix)
auto longInt = 42L; // long (l or L suffix)
auto unsignedLong = 42UL; // unsigned long (ul, UL, uL, or Ul suffix)
auto longLongInt = 42LL; // long long (ll or LL suffix)
auto unsignedLongLong = 42ULL; // unsigned long long (ull, ULL, etc.)

// Numeric bases
auto binaryValue = 0b1010; // Binary literal (C++14): decimal 10
auto octalValue = 052; // Octal literal: decimal 42
auto hexValue = 0x2A; // Hexadecimal literal: decimal 42

// Digit separators for readability (C++14)
auto largeValue = 1'000'000'000; // One billion
auto hexBytes = 0xFF'FF'FF'FF; // Four bytes as hex
auto binFlags = 0b1010'0110'1110; // Binary with separators
```

## Integer Type Selection Guidelines

When choosing an integer type, consider:

1. **Use `int` for general-purpose integers** - It's typically the most efficient type for the platform
2. **Use fixed-width types for portability** - When specific sizes are required across platforms
3. **Use `size_t` for sizes and indices** - For array indices, container sizes, and loop counters
4. **Use `ptrdiff_t` for pointer differences** - When calculating offsets or pointer arithmetic
5. **Use unsigned types for non-negative values** - When negative values don't make sense (e.g., counts)
6. **Use `long long` for very large integers** - When the value might exceed 2 billion
7. **Consider memory constraints** - Use smaller types when memory is limited and values fit

## Real-World Use Cases

### Game Development

```cpp
// Game entity position on a tile map
int16_t tileX{-120}; // Signed because position can be negative
int16_t tileY{85};

// Player statistics
uint16_t health{100}; // Health points (0-65535)
uint8_t level{42}; // Player level (0-255)
uint32_t experiencePoints{1234567}; // XP can be large

// Game flags packed in bits
uint8_t playerFlags{0};
playerFlags |= (1 << 0); // Invulnerable
playerFlags |= (1 << 2); // Has special item
```

### Network Programming

```cpp
// Protocol message header
struct MessageHeader {
    uint8_t version; // Protocol version
    uint8_t type; // Message type
    uint16_t length; // Payload length (0-65535 bytes)
    uint32_t sequenceNum; // Message sequence number
};

// IPv4 address representation
uint8_t ipOctets[4]{192, 168, 0, 1};
uint32_t ipAddress{
    (ipOctets[0] << 24) | (ipOctets[1] << 16) |
    (ipOctets[2] << 8) | ipOctets[3]
};
```

### Embedded Systems

```cpp
// Sensor data with memory constraints
struct SensorData {
    int16_t temperature; // Temperature in 0.1°C (-3276.8°C to 3276.7°C)
    uint16_t humidity; // Relative humidity in 0.1% (0% to 100%)
    uint8_t batteryLevel; // Battery percentage (0-100%)
};

// Device register manipulation
volatile uint8_t *controlRegister{reinterpret_cast<uint8_t *>(0x40020000)};
*controlRegister |= (1 << 4); // Set bit 4 to enable a feature
*controlRegister &= ~(1 << 2); // Clear bit 2 to disable a feature
```

## Best Practices

1. **Be cautious with unsigned types** - Underflow leads to very large values

   ```cpp
   unsigned int count{10};
   count -= 20;  // Wraps around to 4294967286, not -10
   ```

2. **Check for overflow in calculations** - Integer overflow is undefined behavior for signed types

   ```cpp
   int a{std::numeric_limits<int>::max()};
   int b{2};
   // Check before potentially overflowing
   if (a > std::numeric_limits<int>::max() - b) {
       std::cout << "Would overflow!\n";
   }
   ```

3. **Avoid mixing signed and unsigned types** - This can lead to unexpected conversion issues

   ```cpp
   unsigned int a{10};
   int b{-20};
   if (a > b) { // b gets converted to unsigned, becomes a large positive number!
       std::cout << "This will always print!\n";
   }
   ```

4. **Use `auto` with literal suffixes** - Let the compiler deduce the type based on the literal

   ```cpp
   auto unsignedValue{42U};
   auto longLongValue{1'000'000'000'000LL};
   ```

5. **Use digit separators for readability** - Makes large numbers more readable

   ```cpp
   int largeNumber{1'000'000'000};  // Much clearer than 1000000000
   ```

6. **Use fixed-width types for binary data** - Ensures consistent serialization across platforms

   ```cpp
   struct FileHeader {
       uint32_t magicNumber;
       uint16_t version;
       uint32_t dataOffset;
   };
   ```
