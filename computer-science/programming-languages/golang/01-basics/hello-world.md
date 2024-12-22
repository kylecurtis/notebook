# Hello, World

The "Hello, World" program is the classic starting point for learning any programming language. In Go, it is simple yet provides an excellent opportunity to understand the basics of the language structure and its components.

<br>

---

<br>

## Full Code Example

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

<br>

---

<br>

## Code Breakdown

### 1. `package main`

- **Purpose**: Defines the package as `main`.
  - In Go, every executable program must have a `main` package.
  - This is the entry point of the program and signals that it can be compiled into an executable.

### 2. `import "fmt"`

- **Purpose**: Imports the `fmt` package.
  - `fmt` stands for "format" and is a standard library package.
  - Provides input/output functions such as printing to the console and scanning input.
  
### 3. `func main()`

- **Purpose**: Defines the main function.
  - The `main` function is the entry point of execution in a Go program.
  - It does not accept arguments and does not return any values.
  - When you run the program, the Go runtime executes this function first.

### 4. `fmt.Println("Hello, World!")`

- **Purpose**: Prints the string `"Hello, World!"` followed by a newline to the console.
  - **`fmt.Println`**: A function in the `fmt` package that outputs its arguments to the console.
  - **`"Hello, World!"`**: A string literal enclosed in double quotes.
  - The `Println` function adds a newline (`\n`) at the end of the output.

<br>

---

<br>

## Key Concepts to Master

### Go Packages

- Packages group related code into modular units.
- The `main` package is special because it makes a program executable.
- Use the `import` keyword to include standard library packages or your custom packages.

### Functions

- Functions in Go are defined using the `func` keyword.
- The `main` function is a predefined convention for the program's entry point.

### Strings

- Strings are sequences of characters enclosed in double quotes.
- They can include escape sequences like `\n` for newlines.

### Printing to Console

- The `fmt` package provides functions like:
  - `fmt.Print()`: Outputs text without a newline.
  - `fmt.Println()`: Outputs text with a newline.
  - `fmt.Printf()`: Formats and prints text.

<br>

---

<br>

## Common Mistakes to Avoid

1. Forgetting `package main`:
   - Without the `main` package, the program won’t compile as an executable.
2. Missing `func main()`:
   - If there’s no `main` function, the Go runtime has nothing to execute.
3. Incorrect imports:
   - Ensure the package name is in quotes, e.g., `"fmt"`.

<br>

---

<br>

## Summary

- **Packages**: Define the scope of the program.
- **Imports**: Include functionality from Go's standard library.
- **Functions**: Encapsulate logic and define the program’s execution flow.
- **Printing**: Use the `fmt` package to display output.
