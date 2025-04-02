# Variables and Constants in C++

Variables and constants are fundamental building blocks in C++ programming. They allow us to store, access, and manipulate data throughout our programs.

## Variables

A variable is a named storage location in memory that holds a value of a specific type. The value can be changed during program execution.

### Declaration vs Definition

In C++, it's important to understand the distinction between declaring and defining a variable:

-   **Declaration**: Introduces a variable name and its type without allocating memory
-   **Definition**: Allocates memory for the variable

```cpp
// Declaration only (in a header file)
extern int marketCount;

// Definition (in a source file)
int marketCount = 100;
```

Most of the time, variables are both declared and defined in a single statement.

### Variable Declaration Syntax

The basic syntax for variable declaration:

```cpp
type variable_name; // Declaration
type variable_name = value; // Declaration with copy initialization
```

### Variable Initialization

#### Default Initialization

When a variable is declared without an initializer:

```cpp
int stockPrice; // Uninitialized (contains garbage value)
```

Default initialization leaves fundamental types (like `int`) with indeterminate values. Classes may have default constructors that initialize them properly.

#### Value Initialization

Initializes the variable with the type's default value (usually zero for fundamental types):

```cpp
int tradeVolume{}; // Initialize with default value (0 for numeric types)
std::string tickerSymbol{}; // Empty string
```

#### Direct Initialization

Uses parentheses to initialize a variable:

```cpp
int portfolioValue(10000); // Functional style initialization
std::string currencyPair("USD/EUR"); // Constructor-like initialization
```

#### Copy Initialization

Uses the assignment operator syntax:

```cpp
int shareCount = 100; // Old style, less preferred
std::string assetClass = "Equity"; // Copy initialization
```

#### Direct List Initialization (C++11)

Uses curly braces, preventing narrowing conversions (preferred in modern C++):

```cpp
int tradeCount{8}; // Modern style, type-safe
double interestRate{4.25}; // Prevents narrowing conversions

// Example of narrowing conversion prevention
// int bondYield{4.5}; // Error: narrowing conversion
int bondYield = 4.5; // Works but loses precision silently
```

#### Aggregate Initialization

For arrays and structs, initializes members in order:

```cpp
struct StockInfo {
    std::string ticker;
    double price;
    int volume;
};

// Aggregate initialization
StockInfo appleStock{"AAPL", 187.5, 12500000};

// Array initialization
int quarterlyReturns[]{2, 5, -3, 7};  // Returns in percent for Q1-Q4
```

#### Reference Initialization

References must be initialized at declaration:

```cpp
int sharePrice{150};
int& applePrice{sharePrice}; // Reference must be initialized

const int& fixedRate{sharePrice / 10}; // Reference to const
```

### Why Direct List Initialization is Preferred

1. **Prevents narrowing conversions**: Won't implicitly convert between types that could lose data
2. **Uniform syntax**: Works consistently across different types
3. **No most vexing parse issues**: Avoids ambiguities in complex declarations
4. **Zero initialization**: Using empty braces `{}` ensures default initialization

### Variable Naming Conventions

While C++ doesn't enforce specific naming conventions, here are common practices:

-   **camelCase**: First word lowercase, subsequent words capitalized (e.g., `stockPrice`)
-   **snake_case**: All lowercase with underscores (e.g., `market_cap`)
-   **PascalCase**: All words capitalized (e.g., `StockPortfolio`)
-   **ALL_CAPS**: For constants (e.g., `RISK_FREE_RATE`)

Identifiers should be descriptive and meaningful. Avoid abbreviations unless they're widely understood.

## Type Deduction and Aliases

### auto Type Deduction (C++11)

The `auto` keyword deduces a variable's type from its initializer:

```cpp
auto indexValue{5423}; // Deduced as int
auto price{42.75}; // Deduced as double
auto ticker{"MSFT"}; // Deduced as const char*
```

#### auto with References and Qualifiers

```cpp
auto& bondYield{yieldCurve}; // Reference to the original variable
const auto& fixedRate{riskFreeRate}; // Const reference

auto* portfolioPtr{&portfolio}; // Pointer type deduction
```

#### Trailing Return Types

```cpp
// Regular function syntax
double calculatePortfolioReturn(double initialValue, double finalValue);

// Trailing return type syntax (useful with complex return types)
auto calculatePortfolioReturn(double initialValue, double finalValue) -> double;
```

#### auto Return Types (C++14)

```cpp
auto getStockByIndex(int index) {
    return stockList[index]; // Return type deduced from return statement
}
```

### decltype (C++11)

The `decltype` keyword evaluates the type of an expression without executing it:

```cpp
int tradeCount{150};
decltype(tradeCount) orderCount{75}; // orderCount has same type as tradeCount

// Complex case
decltype(tradeCount + 0.0) averagePrice{42.75}; // double (due to type promotion)
```

#### decltype(auto) (C++14)

Combines `auto` and `decltype` semantics, preserving references and cv-qualifiers:

```cpp
template<typename Container>
decltype(auto) getFirstAsset(Container& c) {
    return c[0];  // Preserves reference-ness of the return type
}
```

#### decltype Rules and Edge Cases

```cpp
int marketCap{1000000};
int& marketCapRef{marketCap};

decltype(marketCap) cap1; // int
decltype(marketCapRef) cap2{marketCap}; // int&
decltype((marketCap)) cap3{marketCap}; // int& (parenthesized id is lvalue expression)
```

### Type Aliases

#### typedef (Traditional Way)

```cpp
typedef double Dollars;
typedef int QuarterlyReturns[4]; // Array of 4 ints

Dollars accountBalance{10452.75};
```

#### using (C++11)

```cpp
using Percentage = double;
using PriceVolumePair = std::pair<double, int>;

Percentage annualReturn{12.5};
PriceVolumePair dailyData{145.8, 3250000};
```

The `using` syntax is more flexible than `typedef`, especially with templates:

```cpp
// Template alias (harder with typedef)
template<typename T>
using PriceHistory = std::vector<T>;

PriceHistory<double> stockPrices;
```

## Constants

Constants are variables whose values cannot be changed after initialization. C++ provides several ways to define constants.

### const

The `const` keyword creates a compile-time constant that cannot be modified after initialization.

```cpp
// Compile-time constant
const double TAX_RATE{0.15};

// TAX_RATE = 0.20; // Error: cannot modify a const

int tradingDays{252};
const int ANNUAL_TRADING_DAYS{tradingDays}; // Runtime value, compile-time constant
```

### constexpr (C++11)

The `constexpr` keyword explicitly creates a compile-time constant that must be evaluated at compile time.

```cpp
constexpr double USD_TO_EUR{0.92}; // Evaluated at compile time

// A simple constexpr function
constexpr double convertCurrency(double amount, double rate) {
    return amount * rate;
}

constexpr double INVESTMENT_AMOUNT{10'000.00}; // Note: C++14 digit separators
constexpr double INVESTMENT_EUR{convertCurrency(INVESTMENT_AMOUNT, USD_TO_EUR)}; // Compile-time calculation
```

### constinit (C++20)

The `constinit` keyword ensures a variable has static initialization (initialized at compile time), but doesn't make it constant—the value can be changed later.

```cpp
// Global variables demonstration
constinit double marketOpenPrice{145.75}; // Must be initialized at compile time
// constinit double currentPrice{getLatestPrice()}; // Error: not a constant expression

// constinit only applies to variables with static or thread storage duration
// constinit int localVar{42}; // Error: constinit not allowed here

marketOpenPrice = 146.25; // Unlike const, can be modified
```

## Comparison of Constants

| Feature                | const              | constexpr             | constinit                   |
| ---------------------- | ------------------ | --------------------- | --------------------------- |
| When evaluated         | Compile or runtime | Compile time only     | Compile time initialization |
| Can be modified        | No                 | No                    | Yes                         |
| Can use runtime values | Yes                | No                    | No                          |
| Where usable           | Any variable       | Variables & functions | Static/thread storage only  |
| Introduced in          | C++98              | C++11                 | C++20                       |

## Best Practices

1. **Use direct list initialization `{}` when defining variables**
2. **Prefer `constexpr` over `const` for compile-time constants**
3. **Use `const` for values that shouldn't change but aren't known at compile time**
4. **Use `constinit` for global/static variables that need compile-time initialization but runtime modification**
5. **Use meaningful names that reflect the purpose of the variable**
6. **Initialize variables at the point of declaration**
7. **Use `auto` when the type is obvious from the initialization**
8. **Avoid unnecessary type aliases that don't add clarity**
