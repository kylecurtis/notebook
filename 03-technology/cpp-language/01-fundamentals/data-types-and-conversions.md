## C++ Fundamental Data Types

<br>

### Boolean

- Keyword: `bool`
- Size: Usually 1 byte (implementation-defined)
- Possible values: `true` / `(1)` or `false` / `(0)`

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

### Character

- Keyword: `char`
- Size: At least 8 bits (1 byte)

> In C++, `char` is primarily used for representing characters, but it's also an integer type. The reason for having both signed and unsigned versions is:
>
> **Representation needs**: Some systems might use signed chars to represent values from -128 to 127, while others might use unsigned chars for values from 0 to 255.
>
> **Portability concerns**: The C++ standard doesn't specify whether plain `char` is signed or unsigned by default - it's implementation-defined. This can lead to different behavior across different compilers and platforms.

|Type|Keyword|Size|Range|Signed|
|---|---|---|---|---|
|Character|`char`|8 bits (1 byte)|-128 to 127 or 0 to 255|Implementation-defined|
|Signed character|`signed char`|8 bits (1 byte)|-128 to 127|Yes|
|Unsigned character|`unsigned char`|8 bits (1 byte)|0 to 255|No|
|UTF-8 character|`char8_t` (C++20)|8 bits (1 byte)|0 to 255|No|
|UTF-16 character|`char16_t` (C++11)|At least 16 bits (2 bytes)|0 to 65,535|No|
|UTF-32 character|`char32_t` (C++11)|At least 32 bits (4 bytes)|0 to 4,294,967,295|No|

```cpp
char char_normal = 'a';
```

<br>

### Wide Character

- Keyword: `wchar_t`
- Size: Typically 2 bytes (Windows) or 4 bytes (Unix/Linux)

|Type|Keyword|Size|Range|Signed|
|---|---|---|---|---|
|Wide character|`wchar_t`|Platform-dependent|Platform-dependent|Platform-dependent|



