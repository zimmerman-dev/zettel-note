 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚10:09 pm  📆 Wed Sep 17
 🔗 **Related Concepts**: #note #cpp
___
## 📝 Note: Literals
Consider the following two statements:
```cpp
std::cout << "Hello world!";
int x { 5 };
```
> `"Hello world!"` is a **string literal**, and `5` is an **integer literal**.  
`x` is **not** a literal — it’s a variable initialized **with** a literal. // NEW clarification
### 🔹 Key insight
- Literals are values that are inserted directly into the source code. These values usually appear directly in the executable code (unless they are optimized out).
- Objects and variables represent memory locations that hold values. These values can be fetched on demand.
### 🔹 Types of Literals

|**Type**|**Example**|**Description**|
|---|---|---|
|Integer|`42`, `-7`, `0xFF`|Whole numbers (decimal, hex, octal, binary)|
|Floating-point|`3.14`, `-0.5f`|Decimal numbers with fractions|
|Boolean|`true`, `false`|Logical truth values|
|Character|`'A'`, `'\n'`|Single characters|
|String|`"Hello"`, `"Hi\n"`|Sequences of characters|
### 🔹 Literal Suffixes
If the default type of a literal is not as desired, you can change the type of a literal by adding a suffix. Most suffixes are **not case sensitive**. The most common are as follows:

|   Data Type    |            Suffix            |           Meaning            |
| :------------: | :--------------------------: | :--------------------------: |
|    Integral    |          `u` or `U`          |        `unsigned int`        |
|    Integral    |          `l` or `L`          |            `long`            |
|    Integral    | `ul`, `UL`, `uL`, `Ul`, etc. |       `unsigned long`        |
|    Integral    |         `ll` or `LL`         |         `long long`          |
|    Integral    |  `ull`, `ULL`, `Ull`, etc.   |     `unsigned long long`     |
|    Integral    |          `z` or `Z`          | `signed std::size_t` (C++23) |
|    Integral    |    `uz`, `UZ`, `uZ`, etc.    |    `std::size_t` (C++23)     |
| Floating-point |          `f` or `F`          |           `float`            |
| Floating-point |          `l` or `L`          |        `long double`         |
|     String     |             `s`              |        `std::string`         |
|     String     |             `sv`             |      `std::string_view`      |
#### Noteworthy
- for literal suffix `L`, consider using the uppercase for readability purposes.
- **In most cases,** suffixes aren't need unless it's a `float`.
- `s` and `sv` are covered more in the introduction to `std::string_view` in [[string]].
- See where suffixes get a lot of use here, in [[Keyword - auto]].
### 🔹 Integral Literals
You generally won't need to use suffixes for integral literals. In most cases, it's fine to use non-suffixed `int` literals, even when initializing non-`int` types:
```cpp
int main() {
    int a{5};           // OK: Types match
    unsigned int b{6};  // OK: Compiler will convert int value 6 to unsigned int value 6
    long c{7};          // OK: Compiler will convert int value 7 to long value 7
    return 0;
}
```

In these cases, the compiler will convert the `int` literal to the appropriate type.
### 🔹 Floating-point literals
As we already know, floating point literals without a suffix will always be double unless otherwise stated.
```cpp
#include <iostream>

int main()
{
    std::cout << 5.0 << '\n';  // 5.0 (no suffix) is type double (by default)
    std::cout << 5.0f << '\n'; // 5.0f is type float

    return 0;
}
```
#### Scientific Notation for floating-point literals
In standard notation, we write literals with a decimal point:
```cpp
double pi{3.14159};
```

In scientific notation, we write literals with an `e` to represent the exponent:
```cpp
double avogadro{6.02e23}; // 6.02 x 10^23
double protonC{1.6e-19};  // 1.6 x 10^-19
```
### 🔹 String Literals
In programming, a **string** is a collection of sequential characters used to represent a *string* of text (such as names, words, sentences, etc.). When you write a "Hello, World!" program, it is most likely by using a string literal.

```cpp
int main() {
  std::cout << "--> Everything inside the double quotes is a string Literal! <--" << '\n';
  return 0;
}
```

While most modern programming languages have strings as fundamental data types, for historical reasons, that is not the case for C++. Rather, they have a strange, complicated type that is





















___
### 📌 Key Definitions










___
### 🧠 Flashcards

