## Characters

- Keyword: `char`
- Size: At least 8 bits (1 byte)
- Can be signed or unsigned by default (implementation-defined)

> In C++, `char` is primarily used for representing characters, but it's also an integer type. The reason for having both signed and unsigned versions is:
>
> **Representation needs**: Some systems might use signed chars to represent values from -128 to 127, while others might use unsigned chars for values from 0 to 255.
>
> **Portability concerns**: The C++ standard doesn't specify whether plain `char` is signed or unsigned by default - it's implementation-defined. This can lead to different behavior across different compilers and platforms.

<br>

### Character Table 

| Type               | Keyword            | Size                       | Range                   | Signed                 |
| ------------------ | ------------------ | -------------------------- | ----------------------- | ---------------------- |
| Character          | `char`             | 8 bits (1 byte)            | -128 to 127 or 0 to 255 | Implementation-defined |
| Signed character   | `signed char`      | 8 bits (1 byte)            | -128 to 127             | Yes                    |
| Unsigned character | `unsigned char`    | 8 bits (1 byte)            | 0 to 255                | No                     |


### UTF Character Table

| Type               | Keyword            | Size                       | Range                   | Signed                 |
| ------------------ | ------------------ | -------------------------- | ----------------------- | ---------------------- |
| UTF-8 character    | `char8_t` (C++20)  | 8 bits (1 byte)            | 0 to 255                | No                     |
| UTF-16 character   | `char16_t` (C++11) | At least 16 bits (2 bytes) | 0 to 65,535             | No                     |
| UTF-32 character   | `char32_t` (C++11) | At least 32 bits (4 bytes) | 0 to 4,294,967,295      | No                     |

<br>

### Character Literal Syntax

Character literals use different syntax:

- char: `'a'`
- wchar_t: `L'a'`
- char8_t: `u8'a'` (Note: only ASCII characters allowed in `u8''` literals before C++23)
- char16_t: `u'a'` or `u'\uXXXX'`
- char32_t: `U'a'` or `U'\UXXXXXXXX'`

<br>

**ASCII Character Examples** 

```cpp
// Represents 'A' in the source/execution encoding
char letter = 'A';
```

```cpp
// Represents 'A' using wchar_t encoding 
wchar_t wide_letter = L'A';
```

```cpp
// Represents 'A' as a UTF-8 code unit (C++20)
char8_t utf8_a = u8'A';
```

```cpp
// Represents 'A' as a UTF-16 code unit
char16_t utf16_a = u'A';
```

```cpp
// Represents 'A' as a UTF-32 code unit (Code Point)
char32_t utf32_a = U'A';
```

<br>

**Non-ASCII Character Examples**

```cpp
// Japanese character 'hon' (book) - U+672C  
char16_t kanji = u'本';

// Equivalent using hex escape
char16_t kanji_hex = u'\u672C';
```

```cpp
// Whale emoji - U+1F433
char32_t emoji = U'🐳';

// Equivalent using hex escape
char32_t emoji_hex = U'\U0001F433';
```



<br>

### Wide Character

- Keyword: `wchar_t`
- Size: Typically 2 bytes (Windows) or 4 bytes (Unix/Linux) - **Platform Dependent!**
- Not recommended for portable code unless interacting with platform APIs (like WinAPI) that require it.

| Type           | Keyword   | Size               | Range              | Signed             |
| -------------- | --------- | ------------------ | ------------------ | ------------------ |
| Wide character | `wchar_t` | Platform-dependent | Platform-dependent | Platform-dependent |

<br>

### Character Encoding Systems

**ASCII**

- 7-bit encoding (0-127)
- Only covers English letters, numbers, basic punctuation
- Cannot represent most non-English characters or symbols. **Superseded by Unicode.**

**Unicode**

Unicode vastly expands beyond ASCII's limited range. It defines **Code Points** (unique numbers) for characters. **Encodings** (like UTF-8, UTF-16, UTF-32) define how these code points are represented as sequences of bytes (**Code Units**).

- **Code Point:** The abstract number for a character (e.g., U+1F433 for 🐳).
- **Code Unit:** The basic element of storage in an encoding (e.g., a `char8_t` for UTF-8, a `char16_t` for UTF-16). A single Code Point might require multiple Code Units.
- **Grapheme Cluster:** What a user perceives as a single character (e.g., 'e' + combining accent '´' = 'é'). Can be multiple code points.

**Typical Encoding Intention**

- `char`: The _execution_ encoding (often locale-dependent, UTF-8 on modern Linux/macOS, potentially legacy codepages on Windows unless `/utf-8` flag is used). **Risky for portable Unicode.**
- `char8_t`: **Always** a UTF-8 code-unit. **Recommended for portable UTF-8 text.**
- `char16_t`: A UTF-16 code-unit. Used by Windows API, Java, JavaScript internally.
- `char32_t`: A UTF-32 code-unit, which is large enough to hold any single Unicode **code point**.
- `wchar_t`: Platform-dependent (often UTF-16 on Windows, UTF-32 on Linux). Avoid for portable code.

<br>

### Unicode Character Types & Literals

#### char8_t (UTF-8)

- Stores **one byte** (code unit) of a UTF-8 sequence.
- Characters beyond ASCII (U+007F) require **multiple `char8_t`** code units.

```cpp
// In UTF-8, 🐳 (U+1F433) is represented by 4 bytes: F0 9F 90 B3

// Using an array of char8_t:
char8_t whale_utf8_bytes[] = { u8'\xF0', u8'\x9F', u8'\x90', u8'\xB3', u8'\0' }; // Null-terminated

// Using a string literal (compiler handles the encoding):
const char8_t* whale_str8 = u8"🐳"; // Pointer to the first byte of the 4-byte sequence + null terminator
```

<br>

#### char16_t (UTF-16)

- Stores **one 16-bit code unit** of a UTF-16 sequence.
- Code points outside the Basic Multilingual Plane (BMP, U+0000 to U+FFFF) require **two `char16_t`** code units (a **surrogate pair**).

```cpp
// 🐳 (U+1F433) is outside the BMP. In UTF-16, it's a surrogate pair: D83D DC33

// Using individual char16_t:
char16_t whale_surrogate_high = u'\uD83D'; // High surrogate
char16_t whale_surrogate_low  = u'\uDC33'; // Low surrogate

// Using an array (string):
char16_t whale_char16_arr[] = { u'\uD83D', u'\uDC33', u'\0' }; // Null-terminated

// Using a string literal:
const char16_t* whale_str16 = u"🐳"; // Pointer to the first code unit (D83D)
```

<br>

#### char32_t (UTF-32)

- Stores **one 32-bit code unit**, which is large enough to hold **any single Unicode code point**.
- Simplifies indexing by code point, but uses more memory (4 bytes per character).

```cpp
// 🐳 (U+1F433) fits in a single char32_t

// Direct Literal:
char32_t whale_char32 = U'🐳';

// Universal Character Name:
char32_t whale_char32_ucn = U'\U0001F433';

// Hexadecimal Value:
char32_t whale_char32_hex = 0x1F433; // Same value

// Using a string literal:
const char32_t* whale_str32 = U"🐳"; // Pointer to the single code point + null terminator
```

<br>

### Unicode String Types

#### std::string (Use with Caution for Unicode)

- Stores `char`. Its encoding is **locale/compiler-dependent**.
- **Only reliably holds UTF-8 if the source file is UTF-8 encoded AND the compiler is configured correctly (e.g., `/utf-8` on MSVC).** Highly prone to portability issues otherwise.
```cpp
// Assumes source file is UTF-8 and compiler interprets literals correctly
std::string whale_string = "🐳"; // Contains the 4 bytes F0 9F 90 B3

// Using hex escape sequence (less readable, but explicit):
std::string whale_string_esc = "\xF0\x9F\x90\xB3"; // Manually specify UTF-8 bytes
```

> **Portability Warning:** Relying on `std::string` for Unicode text is fragile. If the execution environment doesn't match the assumed encoding, the string data will be misinterpreted. Prefer `std::u8string` for reliable UTF-8 handling.

<br>

#### std::u8string (C++20) - Recommended for UTF-8

- Stores `char8_t`. Explicitly designed for UTF-8.

```cpp
// UTF-8 encoded string
std::u8string whale_u8string = u8"🐳";
```

<br>

#### std::u16string

- Stores `char16_t`. Explicitly designed for UTF-16.

```cpp
// UTF-16 encoded string using the u prefix
std::u16string whale_u16string = u"🐳"; // Contains the surrogate pair D83D DC33
```

<br>

#### std::32string (C++11)

- Stores `char32_t`. Explicitly designed for UTF-32.

```cpp
// UTF-32 encoded string using the U prefix
std::u32string whale_u32string = U"🐳"; // Contains the single code point 1F433
```

<br>

### Limitations of Standard Library for Unicode Processing

While C++ provides types to _store_ Unicode strings, the standard library lacks robust functions for _processing_ them correctly according to Unicode rules.

- **Case Conversion:** `std::toupper`/`std::tolower` work on single `char` based on locale and don't handle multi-byte characters or language-specific rules (e.g., Turkish 'i').
- **Normalization:** Comparing strings like "é" (precomposed) and "e" + "´" (combining mark) requires Unicode normalization, which isn't built-in.
- **Grapheme Cluster Iteration:** Iterating by what users _see_ as characters requires special logic not present in standard iterators.
- **Searching/Splitting:** Standard find/split functions operate on code units, which may incorrectly break characters.

> **Note:** For complex Unicode tasks (correct case folding, normalization, collation, segmentation by word/sentence/grapheme), use dedicated libraries like [ICU (International Components for Unicode)](https://icu.unicode.org/), [Boost.Text](https://www.boost.org/doc/libs/release/libs/text/doc/html/index.html), or smaller focused libraries (e.g., utf8proc).

<br>

### Using Named Character Escapes (C++23)

A recent addition allowing characters to be specified by their official Unicode name. Requires C++23 support.

```cpp
// Using Unicode character name (requires C++23 compiler)

const char* whale_named = "\N{SPUTING WHALE}";
const char8_t* whale_named_u8 = u8"\N{SPUTING WHALE}";
const char16_t* whale_named_u16 = u"\N{SPUTING WHALE}";
const char32_t* whale_named_u32 = U"\N{SPUTING WHALE}";
```

<br>

## Printing Unicode

The key challenges are:

1. Ensuring your string data is correctly encoded (usually UTF-8).
2. Ensuring the C++ runtime and the terminal/console agree on the encoding for output.

### Scenario 1: Using `std::print` (C++23 and later) 

> Recommended Modern Approach

`std::print` is designed to be more aware of encoding issues and generally aims for "it just works" behavior, especially with UTF-8.

**Best Practice:**

1. **Use UTF-8 encoded string literals:** Prefer `u8"..."` literals, which produce `const char8_t*`. Store them in `std::u8string` (C++20) or use the literals directly.
2. **Ensure Source File Encoding:** Save your source files as UTF-8.
3. **Ensure Compiler Interpretation:** Use compiler flags if necessary to ensure string literals are treated as UTF-8 (e.g., `/utf-8` for MSVC; often the default for GCC/Clang on Linux/macOS).
4. **Rely on `std::print`:** It typically interacts correctly with the underlying system's locale settings to output UTF-8 appropriately, assuming the terminal supports it.

**Example:**

```cpp
#include <print>
#include <string>

int main() {
    
}
```


<br>

### Setting Up `<print>` for Unicode

- Introduced: C++23

#### Enabling std::print

**For GCC**

- Required GCC Version: 14
- Should work without extra setup


**For Clang**

- Required Clang Version: 18
- For Linux, you may also need to install and use libc++:

```shell
sudo apt-get install libc++-dev libc++abi-dev
```

```shell
sudo pacman -S libc++
```

CMakeLists.txt

```txt
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -stdlib=libc++")  
set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -stdlib=libc++ -lc++abi")
```

- **`libc++-dev` package**: This installed LLVM's C++ standard library (libc++) headers
- **`libc++abi-dev` package**: This installed LLVM's C++ ABI implementation, which handles things like exception handling

The `-stdlib=libc++` flag in your CMake configuration tells Clang to use LLVM's libc++ implementation instead of GCC's libstdc++. Without this flag, Clang defaults to using GCC's libstdc++ on Linux systems.

### Using std::print / std::println

`std::print` provides portable Unicode support. All you need to do is make sure that the string literal encoding is UTF-8. This is normally the default on POSIX and on Windows/MSVC it is enabled with a single compiler switch, `/utf-8`. It is a good idea to use `/utf-8` even if you don’t need `std::print`.

```cpp
#include <print>

int main() {
	std::print
}
```