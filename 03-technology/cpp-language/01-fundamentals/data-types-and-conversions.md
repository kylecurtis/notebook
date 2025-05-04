# C++ Fundamental Data Types

<br>

---

<br>

## Booleans

-   Keyword: `bool`
-   Size: Usually 1 byte (implementation-defined)
-   Possible values: `true` / `1` or `false` / `0`

```cpp
// True booleans
bool is_day = true;
bool is_light = 1;
```

```cpp
// False booleans
bool is_night = false;
bool is_dark = 0;
```

<br>

---

<br>

## Characters

### Character Table

|Type|Keyword|Size|Range|Signed|
|---|---|---|---|---|
|Character|`char`|1 byte|-128 to 127 or 0 to 255|Implementation-defined|
|Signed character|`signed char`|1 byte|-128 to 127|Yes|
|Unsigned character|`unsigned char`|1 byte|0 to 255|No|
|Wide character|`wchar_t`|Platform-dependent|Platform-dependent|Platform-dependent|
|UTF-8 character|`char8_t` (C++20)|1 byte|0 to 255|No|
|UTF-16 character|`char16_t` (C++11)|At least 2 bytes|0 to 65,535|No|
|UTF-32 character|`char32_t` (C++11)|At least 4 bytes|0 to 4,294,967,295|No|

<br>

### Important Character Type Details

- `char` can be signed or unsigned by default (implementation-defined)
- `wchar_t` is typically 2 bytes (Windows) or 4 bytes (Unix/Linux)
- Character literals use different syntax:
    - `char`: `'a'`
    - `wchar_t`: `L'a'`
    - `char8_t`: `u8'a'` (C++20)
    - `char16_t`: `u'a'`
    - `char32_t`: `U'a'`

<br>

### Character Examples

#### char

Represents 'A' in the source/execution encoding

```cpp
char letter = 'A';
```

#### char8_t

Represents 'A' as a UTF-8 code unit (C++20)

```cpp
char8_t utf8_a = u8'A';
```

#### char16_t

Represents 'A' as a UTF-16 code unit

```cpp
char16_t utf16_a = u'A';
```

#### char32_t

Represents 'A' as a UTF-32 code unit (Code Point)

```cpp
char32_t utf32_a = U'A';
```

#### wchar_t

Represents 'A' using wchar_t encoding 

```cpp
wchar_t wide_letter = L'A';
```

<br>

---

<br>

## Integers

### Integer Table

|Type|Keyword|Size|Typical Range|Signed|
|---|---|---|---|---|
|Short integer|`short` or `short int`|At least 2 bytes|-32,768 to 32,767|Yes|
|Unsigned short|`unsigned short`|At least 2 bytes|0 to 65,535|No|
|Integer|`int`|At least 2 bytes (typically 4 bytes)|-2,147,483,648 to 2,147,483,647|Yes|
|Unsigned integer|`unsigned` or `unsigned int`|At least 2 bytes (typically 4 bytes)|0 to 4,294,967,295|No|
|Long integer|`long` or `long int`|At least 4 bytes|-2,147,483,648 to 2,147,483,647 (Windows); -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 (Unix/Linux)|Yes|
|Unsigned long|`unsigned long`|At least 4 bytes|0 to 4,294,967,295 (Windows); 0 to 18,446,744,073,709,551,615 (Unix/Linux)|No|
|Long long|`long long` (C++11)|At least 8 bytes|-9,223,372,036,854,775,808 to 9,223,372,036,854,775,807|Yes|
|Unsigned long long|`unsigned long long` (C++11)|At least 8 bytes|0 to 18,446,744,073,709,551,615|No|

<br>

### Integer Examples

#### short int

```cpp
short short_num{-32768};
short int short_num2{32767};
```

#### unsigned short int

```cpp
unsigned short ushort_num{0};
unsigned short int ushort_num2{65535};
```

#### int

```cpp
int int_num{-2147483648};
```

#### unsigned int

```cpp
unsigned int uint_num{4294967295};
```

#### long

```cpp
long long_num{-9223372036854775808};
long int long_num2{9223372036854775807};
```

#### unsigned long

```cpp
unsigned long ulong_num{};
unsigned long in ulong_num2{};
```

#### long long

```cpp
long long llong_num{};
```

#### unsigned long long

```cpp
unsigned long long ullong_num{};
```

<br>

### Fixed-Width Integer Types (C++11, `<cstdint>`)

|Type|Size|Range|
|---|---|---|
|`int8_t`|1 byte|-128 to 127|
|`uint8_t`|1 byte|0 to 255|
|`int16_t`|2 bytes|-32,768 to 32,767|
|`uint16_t`|2 bytes|0 to 65,535|
|`int32_t`|4 bytes|-2,147,483,648 to 2,147,483,647|
|`uint32_t`|4 bytes|0 to 4,294,967,295|
|`int64_t`|8 bytes|-9,223,372,036,854,775,808 to 9,223,372,036,854,775,807|
|`uint64_t`|8 bytes|0 to 18,446,744,073,709,551,615|

<br>

### Least/Fast Types (C++11, `<cstdint>`)

- `int_least8_t`, `uint_least8_t` - Smallest type with at least 8 bits
- `int_least16_t`, `uint_least16_t` - Smallest type with at least 16 bits
- `int_least32_t`, `uint_least32_t` - Smallest type with at least 32 bits
- `int_least64_t`, `uint_least64_t` - Smallest type with at least 64 bits
- `int_fast8_t`, `uint_fast8_t` - Fastest type with at least 8 bits
- `int_fast16_t`, `uint_fast16_t` - Fastest type with at least 16 bits
- `int_fast32_t`, `uint_fast32_t` - Fastest type with at least 32 bits
- `int_fast64_t`, `uint_fast64_t` - Fastest type with at least 64 bits

<br>

### Special Integer Types

- `intptr_t`, `uintptr_t`: Integer types capable of holding pointer values
- `intmax_t`, `uintmax_t`: Largest available integer types
- `size_t`: Unsigned type for sizes (result of `sizeof` operator)
- `ptrdiff_t`: Signed type for pointer differences