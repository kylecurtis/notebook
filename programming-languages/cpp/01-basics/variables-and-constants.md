# Variables and Constants in C++

Variables and constants are fundamental building blocks in C++ programming. They allow us to store, access, and manipulate data throughout our programs.

## Variables

A variable is a named storage location in memory that holds a value of a specific type. The value can be changed during program execution.

### Variable Declaration and Initialization

There are several ways to declare and initialize variables in C++. Modern C++ emphasizes the use of direct list initialization (also known as uniform initialization) using curly braces.

#### Declaration Syntax

```cpp
type variable_name;
```

#### Initialization Methods

1. Default initialization
```cpp
int orbitalPeriod; // Uninitialized (contains garbage value)
```

2. Copy initialization
```cpp
int starDistance = 149600000; // Old style, less preferred
```

3. Direct initialization
```cpp
int planetMass(5972); // Functional style initialization
```

4. Direct list initialization (preferred in modern C++)
```cpp
int satelliteCount{8}; // Modern style, type-safe
double gravityMs{9.8}; // Prevents narrowing conversions
```

5. Value initialization
```cpp
int meteorCount{}; // Initialize with default value (0 for numeric types)
```

Example of narrowing conversion prevention
```cpp
// int asteroidSize{4.5};   // Error: narrowing conversion
int asteroidSize = 4.5;     // Works but loses precision silently
```

### Why Direct List Initialization is Preferred

1. **Prevents narrowing conversions**: Won't implicitly convert between types that could lose data
2. **Uniform syntax**: Works consistently across different types
3. **No most vexing parse issues**: Avoids ambiguities in complex declarations
4. **Zero initialization**: Using empty braces `{}` ensures default initialization

## Constants

Constants are variables whose values cannot be changed after initialization. C++ provides several ways to define constants.

### const

The `const` keyword creates a compile-time constant that cannot be modified after initialization.

```cpp
#include <iostream>

int main() {
	// Compile-time constant
    const double LIGHT_SPEED_KMS{299792.458};
    
    // LIGHT_SPEED_KMS = 300000.0; // Error: cannot modify a const
    
    int discoveredPlanets{8};
    const int CURRENT_PLANET_COUNT{discoveredPlanets}; // Runtime value, compile-time constant
    
    std::cout << "Light travels at " << LIGHT_SPEED_KMS << " km/s\n";
    
    return 0;
}
```

### constexpr

The `constexpr` keyword explicitly creates a compile-time constant that must be evaluated at compile time.

```cpp
#include <iostream>

constexpr double PARSEC_TO_LIGHTYEAR{3.26156};  // Evaluated at compile time

// A simple constexpr function
constexpr double calculateDistance(double lightYears) {
    return lightYears * 9.461e12;  // Convert to kilometers
}

int main() {
    constexpr double ANDROMEDA_DISTANCE{2'500'000};  // Note: C++14 digit separators
    constexpr double ANDROMEDA_KM{calculateDistance(ANDROMEDA_DISTANCE)};  // Compile-time calculation
    
    std::cout << "Andromeda is " << ANDROMEDA_DISTANCE << " light years away\n";
    std::cout << "That's " << ANDROMEDA_KM << " kilometers\n";
    
    return 0;
}
```

### constinit (C++20)

The `constinit` keyword ensures a variable has static initialization (initialized at compile time), but doesn't make it constant—the value can be changed later.

```cpp
#include <iostream>

// Global variables demonstration
constinit long long solarSystemAge{4'600'000'000};  // Must be initialized at compile time
// constinit int galaxyAge{getCurrentAge()};  // Error: not a constant expression

int main() {
    // constinit only applies to variables with static or thread storage duration
    // constinit int localVar{42};  // Error: constinit not allowed here
    
    solarSystemAge = 4'600'000'001;  // Unlike const, can be modified
    
    std::cout << "Solar system age: " << solarSystemAge << " years\n";
    
    return 0;
}
```

## Comparison of Constants

|Feature|const|constexpr|constinit|
|---|---|---|---|
|When evaluated|Compile or runtime|Compile time only|Compile time initialization|
|Can be modified|No|No|Yes|
|Can use runtime values|Yes|No|No|
|Where usable|Any variable|Variables & functions|Static/thread storage only|
|Introduced in|C++98|C++11|C++20|

## Best Practices

1. **Use direct list initialization `{}` when defining variables**
2. **Prefer `constexpr` over `const` for compile-time constants**
3. **Use `const` for values that shouldn't change but aren't known at compile time**
4. **Use `constinit` for global/static variables that need compile-time initialization but runtime modification**
5. **Use meaningful names that reflect the purpose of the variable**
6. **Initialize variables at the point of declaration**