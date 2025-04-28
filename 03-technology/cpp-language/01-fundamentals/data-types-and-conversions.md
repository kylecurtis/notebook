## C++ Fundamental Data Types

<br>

### Boolean

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

### Character

- Keyword: `char`
- Size: At least 8 bits (1 byte)
- Can be signed or unsigned by default (implementation-defined)

> In C++, `char` is primarily used for representing characters, but it's also an integer type. The reason for having both signed and unsigned versions is:
>
> **Representation needs**: Some systems might use signed chars to represent values from -128 to 127, while others might use unsigned chars for values from 0 to 255.
>
> **Portability concerns**: The C++ standard doesn't specify whether plain `char` is signed or unsigned by default - it's implementation-defined. This can lead to different behavior across different compilers and platforms.

<br>

#### Character Table 

| Type               | Keyword            | Size                       | Range                   | Signed                 |
| ------------------ | ------------------ | -------------------------- | ----------------------- | ---------------------- |
| Character          | `char`             | 8 bits (1 byte)            | -128 to 127 or 0 to 255 | Implementation-defined |
| Signed character   | `signed char`      | 8 bits (1 byte)            | -128 to 127             | Yes                    |
| Unsigned character | `unsigned char`    | 8 bits (1 byte)            | 0 to 255                | No                     |
| UTF-8 character    | `char8_t` (C++20)  | 8 bits (1 byte)            | 0 to 255                | No                     |
| UTF-16 character   | `char16_t` (C++11) | At least 16 bits (2 bytes) | 0 to 65,535             | No                     |
| UTF-32 character   | `char32_t` (C++11) | At least 32 bits (4 bytes) | 0 to 4,294,967,295      | No                     |

<br>

#### Character Types in Practice

1. **For Individual Characters:**
    
    - Plain `char` is commonly used for ASCII characters and simple operations
    - `wchar_t`, `char16_t`, and `char32_t` can reasonably represent individual Unicode characters
    - `char8_t` is rarely used for individual characters, as a single UTF-8 code unit often doesn't represent a complete character
    
2. **For Strings:**
    
    - All character types are primarily used in string contexts:
        - `char` → `std::string` (ASCII or locale-specific text)
        - `char8_t` → `std::u8string` (UTF-8 encoded Unicode)
        - `char16_t` → `std::u16string` (UTF-16 encoded Unicode)
        - `char32_t` → `std::u32string` (UTF-32 encoded Unicode)
        - `wchar_t` → `std::wstring` (wide strings, platform-dependent)

<br>

#### Character Literal Syntax

Character literals use different syntax:

- char: `'a'`
- wchar_t: `L'a'`
- char8_t: `u8'a'`
- char16_t: `u'a'`
- char32_t: `U'a'`

```cpp
char letter = 'a';
char8_t eszett = u8'A';
char16_t kanji = u'本';
char32_t emoji = U'🐳';
```

<br>

#### Wide Character

-   Keyword: `wchar_t`
-   Size: Typically 2 bytes (Windows) or 4 bytes (Unix/Linux)

| Type           | Keyword   | Size               | Range              | Signed             |
| -------------- | --------- | ------------------ | ------------------ | ------------------ |
| Wide character | `wchar_t` | Platform-dependent | Platform-dependent | Platform-dependent |

<br>

#### Character Encoding Systems

**ASCII**

- 7-bit encoding (0-127)
- Only covers English letters, numbers, basic punctuation
- Cannot represent most non-English characters or symbols

**Unicode**

Unicode vastly expands beyond ASCII's limited range. 

It aims to encompass all human writing systems ever used, plus symbolic notations:

- All Latin/Roman alphabets with various diacritics
- Non-Latin scripts (Cyrillic, Greek, Arabic, Hebrew, etc.)
- East Asian scripts (Chinese, Japanese, Korean)
- South and Southeast Asian scripts
- Historical scripts (Egyptian hieroglyphs, cuneiform, etc.)
- Emoji and pictographs
- Technical, mathematical, and special symbols
- Control characters and formatting codes