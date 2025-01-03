## Overview

A `rune` in Go represents a single Unicode code point. While `string` types are used for text in Go, `rune` is essential for dealing with individual characters, especially in multilingual or Unicode-rich contexts.

<br>

---

<br>

## What is a Rune?

- **Definition**: A `rune` is an alias for `int32` and is used to represent a Unicode code point.
- **Purpose**: It is designed to work with characters beyond the basic ASCII set, supporting the full range of Unicode.

### Declaration

- Using the `rune` keyword:

```go
var r rune = 'A'
```

- Using type inference:

```go
r := 'A'
```

### Literal Representation

- Rune literals are enclosed in single quotes (`'`).
- Example:

```go
var letter rune = 'A'    // ASCII character
var emoji rune = '😀'   // Unicode character
var chinese rune = '你'  // Non-ASCII character
```

### Unicode Representation

- Runes internally store Unicode code points:

```go
fmt.Printf("%c %U\n", 'A', 'A') // Outputs: A U+0041
```

<br>

---

<br>

## Rune and ASCII Characters

- All ASCII characters are valid `rune` values, but not all `rune` values are ASCII.
- ASCII characters have code points ranging from `0` to `127`.
- Example:

```go
var r rune = 'B'
fmt.Println(r)           // Outputs: 66 (ASCII code)
fmt.Printf("%c\n", r)    // Outputs: B
```

<br>

---

<br>

## Rune Operations

### Arithmetic Operations

Runes are integers and support arithmetic operations:

- Example:

```go
r := 'A'
r = r + 1
fmt.Printf("%c\n", r) // Outputs: B
```

### Comparisons

Runes can be compared using standard comparison operators:

- Example:

```go
fmt.Println('A' < 'B') // Outputs: true
```

### Iterating Over Strings

Strings in Go are UTF-8 encoded, and you can iterate over them as runes:

- Example:

```go
for i, r := range "Hello, 世界" {
    fmt.Printf("Index %d: Rune %c (U+%04X)\n", i, r, r)
}
```

<br>

---

<br>

## Rune Conversion

### Converting Between Runes and Strings

- **Rune to String**:

```go
r := 'A'
s := string(r)
fmt.Println(s) // Outputs: A
```

- **String to Rune Slice**:

```go
str := "Go"
runes := []rune(str)
fmt.Println(runes) // Outputs: [71 111]
```

### Casting Runes to Integers

- Convert a rune to its Unicode code point (integer):

```go
r := 'A'
fmt.Println(int32(r)) // Outputs: 65
```

<br>

---

<br>

## Functions for Runes

### `unicode` Package

The `unicode` package provides utility functions for working with runes.

#### Check Character Properties

- Check if a rune is a digit:

```go
import "unicode"

fmt.Println(unicode.IsDigit('5')) // true
fmt.Println(unicode.IsDigit('A')) // false
```

- Check if a rune is a letter:

```go
fmt.Println(unicode.IsLetter('A')) // true
fmt.Println(unicode.IsLetter('1')) // false
```

- Check if a rune is a space:

```go
fmt.Println(unicode.IsSpace(' ')) // true
fmt.Println(unicode.IsSpace('A')) // false
```

#### Convert Case

- Convert a rune to uppercase:

```go
fmt.Println(unicode.ToUpper('a')) // Outputs: A
```

- Convert a rune to lowercase:

```go
fmt.Println(unicode.ToLower('A')) // Outputs: a
```

#### Other Properties

- Check if a rune is a control character:

```go
fmt.Println(unicode.IsControl('\n')) // true
```

<br>

---

<br>

## Special Cases with Runes

### Multibyte Characters

Some characters occupy more than one byte in UTF-8 encoding but are still represented as a single rune:

- Example:

```go
str := "你"
fmt.Println(len(str))         // Outputs: 3 (bytes)
fmt.Println(len([]rune(str))) // Outputs: 1 (rune)
```

### Invalid UTF-8

Strings may contain invalid UTF-8 sequences. To ensure safe handling, use the `utf8` package:

- Example:

```go
import "unicode/utf8"

str := "Hello, 世界"
if utf8.ValidString(str) {
    fmt.Println("Valid UTF-8")
}
```

<br>

---

<br>

## Best Practices

1. **Use Runes for Character-Level Operations**:

   - When working with Unicode or multilingual text, convert strings to runes to handle characters accurately.

2. **Leverage the `unicode` Package**:

   - Use `unicode` functions to simplify character classification and manipulation.

3. **Avoid Direct Byte Operations**:

   - Strings are UTF-8 encoded; directly accessing bytes may not represent complete characters.

4. **Validate Input**:

   - Use `utf8.ValidString` to ensure safe handling of potentially malformed UTF-8 data.
