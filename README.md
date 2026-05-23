# Mini Symbolic CAS for Rational Functions

A C++ mini computer algebra system focused on exact symbolic manipulation of rational functions.

This project supports exact rational arithmetic, symbolic expression trees, expression parsing, simplification, polynomial conversion, polynomial operations, factorization over the rational numbers, and exact partial-fraction decomposition.

---

## Features

- Exact rational-number arithmetic
- Symbolic expression representation
- Expression parsing from strings
- Support for integers, rational numbers, symbols, addition, multiplication, and powers
- Polynomial conversion from parsed expressions
- Polynomial addition, subtraction, multiplication, powers, derivatives, evaluation, and long division
- Simplification of expressions
- Factoring over the rational numbers
- Square-free factorization
- Exact partial-fraction decomposition
- Support for repeated linear factors
- Support for quadratic factors when entered in visible factored form
- Exact reconstruction checks for partial-fraction results
- Parser and partial-fraction test suite

---

## Project Purpose

The purpose of this project is to build a small symbolic math engine from scratch in C++.

Unlike a basic calculator, this project works with exact symbolic values instead of relying on floating-point approximations. For example, fractions such as `2/3`, `5/6`, and `8/5` are preserved exactly throughout calculations.

This project demonstrates:

- Object-oriented C++ design
- Expression-tree modeling
- Recursive parsing
- Exact rational arithmetic
- Polynomial algebra
- Symbolic simplification
- Factoring over Q
- Partial-fraction decomposition
- Test-driven validation of symbolic math behavior

---

## Technologies Used

- C++
- Standard Library
- Terminal / Command Line

---

## Project Structure
```
Mini CAS/
├── src/
│   ├── app/
│   │   └── main.cpp
│   ├── core/
│   │   ├── Rational.h
│   │   ├── Rational.cpp
│   │   ├── Polynomial.h
│   │   └── Polynomial.cpp
│   ├── expr/
│   │   ├── Expr.h
│   │   ├── Expr.cpp
│   │   ├── Simplify.h
│   │   └── Simplify.cpp
│   ├── parsing/
│   │   ├── Parser.h
│   │   └── Parser.cpp
│   └── algebra/
│       ├── Factor.h
│       ├── Factor.cpp
│       ├── PartialFractions.h
│       └── PartialFractions.cpp
└── tests/
    └── ParserTests.cpp
```

---

## Core Components

**Rational**

The Rational class provides exact fraction arithmetic.

It supports:

- Addition
- Subtraction
- Multiplication
- Division
- Normalization of fractions
- String conversion
- Comparison operators

Example:
```
2/3 + 5/6 = 3/2
```
**Expr**

The expression system represents symbolic math expressions as an expression tree.

Supported expression types include:

- Integer expressions
- Rational expressions
- Symbol expressions
- Addition expressions
- Multiplication expressions
- Power expressions

This allows the program to represent symbolic expressions such as:
```
(2/3)*x + x^2 - 5
```
**Parser**

The parser converts user-entered strings into symbolic expression trees.

Supported syntax includes:
```
(2/3)*x + x^2 - 5
2x + x(x+1)
x/2 + (x+1)^2
```
The parser supports implicit multiplication, so expressions like 2x and x(x+1) can be understood without requiring every multiplication symbol to be written explicitly.

**Simplify**

The simplifier reduces symbolic expressions by combining compatible terms and simplifying expression structure.

Examples of simplification behavior include:
```
(2/3)*x + (1/3)*x
```
becoming:
```
x
```
It also simplifies products, powers, constants, and repeated symbolic factors.

**Polynomial**

The Polynomial class represents exact polynomials with rational coefficients.

It supports:

- Creating constant polynomials
- Creating the variable polynomial x
- Addition
- Subtraction
- Multiplication
- Scaling
- Powers
- Derivatives
- Evaluation
- Long division
- String formatting

Example polynomial:
```
x^2 + 2/3*x - 5
```
**Factor**

The factoring system provides exact factorization tools over the rational numbers.

It supports:

- Making polynomials monic
- Polynomial greatest common divisor
- Square-free factorization
- Rational-root search
- Factoring over Q
- Formatting linear factors

Example factorization target:
```
(x-3)(x+2)
```
**PartialFractions**

The partial-fraction system decomposes rational functions into exact partial fractions.

Supported denominator structures include:

- Distinct linear factors
- Repeated linear factors
- Linear plus quadratic factors
- Repeated quadratic factors when entered in visible factored form

Example input:
```
(x+5)/((x-3)(x+2))
```
Example output:
```
8/5/(x - 3) - 3/5/(x + 2)
```
---

## Build and Run Program

**CLI build**

Compile with:
```
g++ -std=c++17 -O2 -Wall -Wextra -pedantic \
  main.cpp Rational.cpp Polynomial.cpp Expr.cpp Simplify.cpp Parser.cpp Factor.cpp PartialFractions.cpp \
  -o minicAS
```
Then run with:
```
./minicAS
```
**Xcode build**

Add these .cpp files to Compile Sources:

- `main.cpp`
- `Rational.cpp`
- `Polynomial.cpp`
- `Expr.cpp`
- `Simplify.cpp`
- `Parser.cpp`
- `Factor.cpp`
- `PartialFractions.cpp`

Then build and run using Command + B.

---

## Build and Run the Test Suite

The project includes a test file named:
```
ParserTests.cpp
```
**CLI test build**

Compile tests with:
```
g++ -std=c++17 -O2 -Wall -Wextra -pedantic \
  tests/ParserTests.cpp Rational.cpp Polynomial.cpp Expr.cpp Simplify.cpp Parser.cpp Factor.cpp PartialFractions.cpp \
  -o minicAS_tests
```
Then run with:
```
./minicAS_tests
```
**Xcode test build**

Add tests/ParserTests.cpp either:

- to a separate test target
            or
- temporarily to the main target while debugging

---

## Test Coverage

The test suite checks behavior such as:

- Parser conversion of expressions into polynomials
- Implicit multiplication
- Division by exact numeric literals
- Invalid syntax handling
- Distinct linear partial fractions
- Repeated linear partial fractions
- Linear plus quadratic partial fractions
- Repeated quadratic partial fractions
- Exact reconstruction checks

---

## Example Test Output

Mini-CAS parser + partial fractions tests
```
[PASS] parser converts '(2/3)*x + x^2 - 5' to polynomial
[PASS] polynomial string matches exact expected output
[PASS] parser converts '2x + x(x+1)' to polynomial
[PASS] implicit multiplication simplifies correctly
[PASS] parser rejects invalid syntax
[PASS] distinct linear factor decomposition succeeds
[PASS] distinct linear factor reconstruction passes

Summary:
  passed:  ...
  failed:  0
```
---

## Current limitations

This is still a mini-CAS, not a full computer algebra system.

Current limitations include:

- no full symbolic simplifier/canonicalizer yet
- no transcendental functions (sin, cos, log, exp, etc.)
- no symbolic integration
- no general exact factorization for arbitrary higher-degree polynomials over all algebraic extensions
- quadratic partial fractions work best when the denominator is entered in visible factored form
- no assumptions system
- no matrix/tensor algebra
- no Gröbner basis or multivariate algebra engine
- Roadmap

---

## Future Improvements

Possible future upgrades include:

- a cleaner interactive menu
- support for multiple variables
- symbolic equation solving
- stronger canonical simplification
- richer parser features
- exact irreducible quadratic handling from expanded forms
- full rational-function normalization
- larger test suite
- broader exact factorization support
- arbitrary-precision integer support
- LaTeX output formatting
- file-based input and output
- a formal unit-testing framework
- a graphical or web-based interface

---

## Current Limitations

This project is intentionally a mini-CAS, not a full symbolic algebra system.

Current limitations include:

- Only one symbolic variable, x, is currently targeted for polynomial conversion
- Negative powers are not supported
- General symbolic division is limited
- Trigonometric, logarithmic, exponential, and radical expressions are not supported
- Quadratic-factor support works best when quadratic factors are entered in visible factored form
- Full symbolic equation solving is not included
- Full arbitrary-precision integer support is not currently implemented

---

## Note

This project is meant to teach and demonstrate how symbolic algebra systems are built from the ground up:

- exact arithmetic first
- exact polynomial algebra second
- parsing and simplification third
- factorization and decomposition on top

It is designed as a learning project and a foundation for a more capable symbolic engine later.

---

## License

This project is open source and available for educational use.

--- 

## Screenshot

<img width="865" height="825" alt="Screenshot 2026-05-14 at 05 17 07" src="https://github.com/user-attachments/assets/8864d020-9f95-4bfd-84aa-38cdeda9354e" />
