# Floating-Point Types in C++

Floating-point types represent real numbers using a binary approximation. They are essential in scientific and numerical computations, but their inherent limitations (such as rounding errors) require careful handling.

<br>

---

<br>

## Floating-Point Types and Literals

<br>

### Types and Their Usage

- **float**
    - Typically 32 bits
    - Approximately 7 decimal digits of precision
- **double**
    - Typically 64 bits
    - Approximately 15 decimal digits of precision
- **long double**
    - Size varies by implementation (commonly 80 bits, 128 bits, or the same as double)
    - Greater precision and range than `double`

<br>

### Literal Suffixes

- **Without suffix:**
    - A literal like `3.14` is of type `double` by default.
- **With `f` suffix:**
    - A literal like `3.14f` is explicitly a `float`.
- **With `L` suffix:**
    - A literal like `3.14L` is explicitly a `long double`.

**Example:**

```cpp
float a{3.14f};       // 32-bit float literal
double b{3.14};       // 64-bit double literal (default)
long double c{3.14L}; // long double literal (size varies)
```

<br>

---

<br>

## Floating-Point Ranges and Precision

Below is a comparison table for the common floating-point types:

|Type|Typical Size (bits)|Precision (decimal digits)|Approximate Range|
|---|---|---|---|
|float|32|~7|~1.2e-38 to 3.4e+38|
|double|64|~15|~2.3e-308 to 1.7e+308|
|long double|≥80|~18 (80-bit) / ~33 (128-bit)|Varies; generally larger than double|

_Note:_ The exact size, precision, and range may depend on your compiler and platform.

---

## Formatting Output with `<iomanip>`

To control the number of significant digits when outputting floating-point values, use `<iomanip>` and its manipulators like `std::setprecision`.

**Example:**

```cpp
#include <iostream>
#include <iomanip>

int main() {
    double pi = 3.141592653589793;
    
    // Set the number of significant digits
    std::cout << "Default precision: " << pi << "\n";
    std::cout << "Set precision (5 significant digits): " << std::setprecision(5) << pi << "\n";
    
    // Fixed format: controls the number of digits after the decimal point
    std::cout << "Fixed with 3 decimals: " << std::fixed << std::setprecision(3) << pi << "\n";
    
    return 0;
}
```

- **`std::setprecision(n)`**: Sets the total number of significant digits by default.
- **`std::fixed`**: Forces the use of fixed-point notation, where `setprecision` specifies the number of digits after the decimal.

<br>

---

<br>

## Rounding Issues

- **Binary Representation:**  
    Not every decimal fraction (e.g., 0.1) can be represented exactly in binary. This can lead to small rounding errors.
    
- **Non-Associative Operations:**  
    The order of floating-point operations can affect the result due to cumulative rounding errors.
    
- **Best Practices:**
    
    - Use appropriate data types based on the precision needed.
    - Be cautious with equality comparisons; consider using an epsilon value for floating-point comparisons.
    - Prefer algorithms designed for numerical stability.

<br>

---

<br>

## Special Values: NaN and Inf

Floating-point arithmetic defines several special values as per the IEEE 754 standard:

- **NaN (Not a Number):**  
    Represents undefined or unrepresentable values (e.g., the result of 0.0/0.0).
    
- **Infinity (Inf):**  
    Represents overflow or division by zero (e.g., 1.0/0.0 results in positive infinity).
    

**Example:**

```cpp
#include <iostream>
#include <cmath>  // for std::isnan, std::isinf

int main() {
    double nanValue = 0.0 / 0.0;
    double infValue = 1.0 / 0.0;
    
    std::cout << "nanValue: " << nanValue << '\n';
    std::cout << "infValue: " << infValue << '\n';
    
    if (std::isnan(nanValue)) {
        std::cout << "nanValue is NaN\n";
    }
    
    if (std::isinf(infValue)) {
        std::cout << "infValue is infinity\n";
    }
    
    return 0;
}
```

<br>

---

<br>

## Modern Best Practices

- **Explicit Literals:**  
    Always use literal suffixes (`f` for float, `L` for long double) when a specific type is intended. This improves clarity and prevents implicit type conversions.
    
- **Consistent Initialization:**  
    Use uniform initialization (brace initialization) where possible:
    
    ```cpp
    float x{3.14f};
    double y{3.14};
    long double z{3.14L};
    ```
    
- **Formatting and Output:**  
    Use `<iomanip>` to ensure output is clear and to control precision.
    
- **Handling Rounding and Special Values:**  
    Design numerical algorithms with an awareness of rounding errors. Use helper functions from `<cmath>` (e.g., `std::isnan`, `std::isinf`) to handle special values.

<br>

---

<br>

## Summary

- **Floating-Point Types:**
    - `float`, `double`, and `long double` differ in size, precision, and range.
- **Literals:**
    - Use `3.14f` for `float` and `3.14L` for `long double`. Without a suffix, literals default to `double`.
- **Ranges and Precision:**
    - Refer to the table above for typical values.
- **Output Formatting:**
    - Utilize `<iomanip>` (e.g., `std::setprecision`, `std::fixed`) to control displayed precision.
- **Rounding and Special Values:**
    - Be mindful of inherent rounding issues; handle NaN and Inf appropriately using `<cmath>`.
