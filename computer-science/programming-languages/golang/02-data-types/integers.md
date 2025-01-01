## Overview

Integers are one of the foundational data types in Go. Go supports both signed and unsigned integers in various sizes to accommodate different ranges and memory requirements. This guide will cover the following:

1. Signed Integers (`int`, `int8`, `int16`, `int32`, `int64`)
2. Unsigned Integers (`uint`, `uint8`, `uint16`, `uint32`, `uint64`)
3. Integer methods/functions for operations and conversions.
4. Practical tips and best practices.

<br>

---

<br>

## Signed Integers

- Signed integers can store both positive and negative numbers.
- Declaration Syntax:

```go
var number int
```

<br>

### Types and Ranges

| Type    | Size (in bits)                                                           | Range                                                   |
| ------- | ------------------------------------------------------------------------ | ------------------------------------------------------- |
| `int8`  | 8                                                                        | -128 to 127                                             |
| `int16` | 16                                                                       | -32,768 to 32,767                                       |
| `int32` | 32                                                                       | -2,147,483,648 to 2,147,483,647                         |
| `int64` | 64                                                                       | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| `int`   | Platform-dependent: 32 bits on 32-bit systems, 64 bits on 64-bit systems |                                                         |

<br>

### Declaration Examples

- Using `int` (default size):

```go
var a int = 42
```

- Using specific sizes:

```go
var b int8 = 120
var c int16 = -3000
var d int64 = 9223372036854775807
```

<br>

---

<br>

## Unsigned Integers

- Unsigned integers can store only positive numbers, but with a larger range than signed integers of the same size.
- Declaration Syntax:

```go
var number uint
```

### Types and Ranges

| Type     | Size (in bits)                                                           | Range                           |
| -------- | ------------------------------------------------------------------------ | ------------------------------- |
| `uint8`  | 8                                                                        | 0 to 255                        |
| `uint16` | 16                                                                       | 0 to 65,535                     |
| `uint32` | 32                                                                       | 0 to 4,294,967,295              |
| `uint64` | 64                                                                       | 0 to 18,446,744,073,709,551,615 |
| `uint`   | Platform-dependent: 32 bits on 32-bit systems, 64 bits on 64-bit systems |                                 |

### Declaration Examples

- Using `uint` (default size):

```go
var x uint = 100
```

- Using specific sizes:

```go
var y uint8 = 200
var z uint64 = 18446744073709551615
```

<br>

---

<br>

## Integer Operations

<br>

### Arithmetic Operations

Go supports basic arithmetic operations for integers:

- **Addition**:

```go
sum := a + b
```

- **Subtraction**:

```go
diff := a - b
```

- **Multiplication**:

```go
product := a * b
```

- **Division**:

```go
quotient := a / b
```

- **Modulus**:

```go
remainder := a % b
```

<br>

### Bitwise Operations

Bitwise operations are performed at the binary level:

- **AND**: `a & b`
- **OR**: `a | b`
- **XOR**: `a ^ b`
- **AND NOT**: `a &^ b`
- **Left Shift**: `a << n`
- **Right Shift**: `a >> n`

<br>

---

<br>

## Type Conversion

<br>

### Explicit Type Conversion

Go does not allow implicit type conversion, so you must explicitly convert types:

```go
var a int32 = 42
var b int64 = int64(a)
```

<br>

### Mixing Signed and Unsigned Types

Mixing signed and unsigned integers requires explicit conversion to avoid compile-time errors:

```go
var x int = 10
var y uint = uint(x)
```

<br>

---

<br>

## Standard Library Functions

<br>

#### Absolute Value

- Go does not have a built-in function for absolute values of integers. You can write your own:

```go
func abs(x int) int {
    if x < 0 {
        return -x
    }
    return x
}
```

#### Random Integer Generation

- Use the `math/rand` package:

```go
import "math/rand"

func main() {
    randInt := rand.Intn(100) // Random integer between 0 and 99
    fmt.Println(randInt)
}
```

#### Parsing Integers

- Convert strings to integers using `strconv`:

```go
import "strconv"

func main() {
    num, err := strconv.Atoi("42")
    if err == nil {
        fmt.Println(num) // Outputs: 42
    }
}
```

<br>

---

<br>

## Best Practices

1. **Choose the Appropriate Type**:

   - Use the smallest integer type that fits your needs to save memory.
   - Use `int` or `uint` unless you need a specific size.

2. **Avoid Mixing Signed and Unsigned**:

   - Always convert explicitly when mixing types.

3. **Be Cautious with Overflows**:

   - Go does not detect integer overflows automatically. Use specific sizes carefully.

4. **Use Constants for Literal Values**:

   - Assign constant values directly to avoid unnecessary type conversions.

5. **Understand Platform-Dependent Sizes**:

   - Be aware that `int` and `uint` sizes depend on your system architecture.
