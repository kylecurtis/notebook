## Overview

> A "Hello, World" program in Go serves as an excellent starting point to understand the basic structure of a Go program.

<br>

---

<br>

### Full Example Code

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

### Breaking Down the Structure

#### The `package` Declaration

   - **Purpose**: Defines the package to which the file belongs.
   - **In `main` Package**:
     - The `main` package is a special package in Go. It is required to create an executable program.
     - Files in other packages are used for libraries or modularity, but only `package main` can contain the `main()` function that serves as the entry point.
   - **Syntax**:
     ```go
     package main
     ```
   - **Rules**:
     - Every Go source file must start with a `package` declaration.
     - The `main` package must always be used for programs intended to produce executable binaries.

<br>

---

<br>

#### Import Statements
   - **Purpose**: Import external or standard library packages required by the program.
   - **Syntax**:
     ```go
     import "fmt"
     ```
   - **Key Points**:
     - Enclose imported package names in double quotes.
     - Can import multiple packages using:
       ```go
       import (
           "fmt"
           "os"
       )
       ```
   - **Common Imports in Simple Programs**:
     - `fmt`: For formatted I/O (e.g., `fmt.Println`, `fmt.Printf`).
     - `os`: For operating system interaction.
     - `log`: For logging messages.
   - **Unused Imports**:
     - Go does not allow unused imports, promoting clean code.

<br>

---

<br>

#### The `main` Function
   - **Purpose**: Entry point for a Go executable program.
   - **Syntax**:
     ```go
     func main() {
         // Code to execute
     }
     ```
   - **Key Characteristics**:
     - Defined using the `func` keyword.
     - Must be named `main` and take no parameters.
     - Does not return any values.
   - **Execution**:
     - The `main` function is executed first when running the program using `go run` or after compiling with `go build`.

<br>

---

<br>

#### Using the `fmt` Package
   - **Purpose**: Provides formatted I/O functions.
   - **Key Functions**:
     - `fmt.Println`: Prints output followed by a newline.
       ```go
       fmt.Println("Hello, World!")
       ```
     - `fmt.Printf`: Formats and prints according to a format specifier.
       ```go
       fmt.Printf("Hello, %s!\n", "World")
       ```
   - **Understanding `fmt.Println`**:
     - Automatically adds a newline (`\n`) after the output.
     - Can handle multiple arguments:
       ```go
       fmt.Println("Hello,", "World!")
       ```

<br>

---

<br>

### Compiling and Running the Program

#### **Writing the Code**
   - Create a file named `hello.go`.
   - Copy the "Hello, World" program into the file.

#### **Running the Program**
   - Using `go run`:
     ```sh
     go run hello.go
     ```
     - Executes the code without creating a binary.
   - Using `go build`:
     ```sh
     go build hello.go
     ```
     - Compiles the program into a binary (e.g., `hello`).
     - Run the binary:
       ```sh
       ./hello
       ```

