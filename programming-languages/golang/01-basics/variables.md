## Overview

> Variables and constants are fundamental in Go, allowing developers to store and manage data efficiently. This note focuses on declaring, initializing, and using variables and constants in Go, along with techniques for grouping declarations and understanding scope.

<br>

---

<br>

## Declaring Variables

#### Using the `var` Keyword

- Syntax:
    
    ```go
    var variableName type
    ```
    
- Example:
    
    ```go
    var age int
    var name string
    ```
    
- **Default Values**:
    - Variables in Go have "zero values" when not explicitly initialized:
        - Numeric types: `0`
        - Boolean: `false`
        - String: `""` (empty string)
        - Pointers/interfaces: `nil`

#### **Declaring and Initializing**

- Syntax:
    
    ```go
    var variableName type = value
    ```
    
- Example:
    
    ```go
    var age int = 25
    ```
    

#### Type Inference

- The type can be omitted, and Go infers it from the value:
    
    ```go
    var age = 25
    ```
    

<br>

---

<br>

### Short Variable Declaration (`:=`)

- Syntax:
    
    ```go
    variableName := value
    ```
    
- Example:
    
    ```go
    planet := "Earth"
    moons := 1 
    ```
    
- **Rules**:
    - Must be used inside functions.
    - Automatically infers the variable type.

<br>

---

<br>

### Multiple Variable Declarations

#### Using `var`

- Syntax:
    
    ```go
    var (
        planet string
        moons  int
        isHabitable bool
    )
    ```
    
- Example:
    
    ```go
    var (
        planet = "Earth"
        moons = 1
        isHabitable = true
    )
    ```
    

#### Using Short Declaration

- Syntax:
    
    ```go
    a, b, c := 1, "text", true
    ```
    

<br>

---

<br>

### Scope of Variables

#### Global Variables

- Declared outside functions using `var`.
- Example:
    
    ```go
    var globalVar = "Accessible everywhere"
    ```
    

#### Local Variables

- Declared inside a function and accessible only within that function.
- Example:
    
    ```go
    func example() {
        localVar := "Accessible only here"
    }
    ```
    

#### Block Scope

- Variables declared within a block `{}` are confined to that block.
- Example:
    
    ```go
    {
        blockVar := "Visible only in this block"
        fmt.Println(blockVar)
    }
    ```
    

<br>

---

<br>

## Constants

### Declaring Constants

#### Using `const`

- Syntax:
    
    ```go
    const constantName type = value
    ```
    
- Example:
    
    ```go
    const Pi float64 = 3.14159
    ```
    

#### Type Inference

- Type can be omitted if the value determines the type.
- Example:
    
    ```go
    const Pi = 3.14159
    ```
    

#### Immutable Nature

- Constants cannot be changed after declaration.
- Example:
    
    ```go
    const Hello = "Hello, World!"
    // Hello = "New Value" // This will cause a compile-time error.
    ```
    

<br>

---

<br>

### Untyped Constants

- Constants without a type can adapt to the context in which they are used.
- Example:
    
    ```go
    const Five = 5
    var a int = Five   // Works because `Five` is untyped.
    var b float64 = Five
    ```
    

<br>

---

<br>

### Grouping Constants

- Constants can be grouped for better readability.
- Syntax:
    
    ```go
    const (
        Pi   = 3.14159
        E    = 2.71828
        Phi  = 1.61803
    )
    ```
    

<br>

---

<br>

### `iota` for Enumerations

- **What is `iota`?**:
    - A special identifier for generating sequential constant values.
- Syntax:
    
    ```go
    const (
        A = iota // 0
        B        // 1
        C        // 2
    )
    ```
    
- Example:
    
    ```go
    const (
        Monday = iota + 1
        Tuesday
        Wednesday
    )
    // Monday = 1, Tuesday = 2, Wednesday = 3
    ```
    

<br>

---

<br>

## **4. Best Practices for Variables and Constants**

1. **Use Constants for Fixed Values**:
    
    - Always prefer constants for unchanging data.
    - Example: `const Pi = 3.14`
2. **Group Related Declarations**:
    
    - Use grouping for logically related variables or constants.
3. **Minimize Scope**:
    
    - Declare variables in the smallest scope possible for clarity and safety.
4. **Avoid Unused Variables**:
    
    - Go does not allow unused variables; this ensures clean and intentional code.
5. **Prefer Short Declarations for Readability**:
    
    - Inside functions, use `:=` for brevity:
        
        ```go
        x := 42
        ```
        

<br>

---

<br>

## **5. Common Errors and Troubleshooting**

### **5.1 Variable Not Used**

- **Error**:
    
    ```text
    declared and not used: variableName
    ```
    
- **Solution**: Remove or use the variable.

### **5.2 Redeclaring Variables**

- **Error**: Redeclaring a variable in the same scope.
- **Solution**: Ensure unique names or explicitly use the original variable.

### **5.3 Constants Must Be Compile-Time Values**

- **Error**: Constants cannot be assigned a non-constant value.
- **Solution**: Use only compile-time literals or `iota`.

<br>

---

<br>

## **6. Exercises**

### **Exercise 1: Declare and Use Variables**

- Write a program that declares and uses variables for your name, age, and favorite number.

### **Exercise 2: Group Variables and Constants**

- Group related variables for a product's `name`, `price`, and `quantity`.

### **Exercise 3: Enumerations with `iota`**

- Use `iota` to create a set of constants for the days of the week.

<br>

---

<br>

## **7. Summary**

- Variables in Go are declared using `var` or `:=` and can hold data that changes.
- Constants, declared using `const`, are immutable and useful for fixed values.
- Grouping variables and constants improves readability and structure.
- Go enforces variable usage and immutability of constants, promoting clean and error-free code.

This mastery guide equips you to confidently use variables and constants in Go programs.