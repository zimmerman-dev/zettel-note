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
- Literals often end up embedded directly in your compiled program — unless the compiler optimizes them away.
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

While most modern languages treat strings as built-in types, C++ takes a different path. For historical reasons, it relies on a lower-level system called [[C-Style Strings]]. We won’t dive into them here, but you can learn more in that note — including how string literals interact with null terminators.

The key reason we hold off here is that **string literals behave differently from other literals**. As you’ll see in [[string]], they’re actually **`const` objects** created at program start and guaranteed to live for the entire duration of the program.
### 🔹 Magic Numbers
Imagine stumbling across a number in code with no explanation — just a bare **`4`** sitting in a condition, dictating who gets through the gate. That’s a **magic number**. It’s “magic” because its meaning isn’t obvious; it works, but you’re left guessing _why_ it’s there and what it represents.

Contrast that with a literal that’s been given a name. For instance:

```cpp
int heightInFeet{5}; // The 5 has meaning because it’s tied to 'heightInFeet'
```

Here, the number isn’t mysterious — it’s labeled. But look at this:

```cpp
if (height > 4) {
     std::cout << "You may enter\n"; 
}
```

What’s **`4`** supposed to be? Minimum height for entry? Some arbitrary cutoff? Unless you’ve memorized the rule, the program gives you no clue. That’s the trap: magic numbers hide intent.

In small snippets, they’re just a nuisance. In large systems, they’re a minefield — every unexplained number is another riddle future you (or your teammates) will have to solve.

The fix is simple but powerful: give the number a name. Replace `4` with a constant like `const int minHeight{4};` and suddenly the code explains itself. You’re not just writing instructions for a computer — you’re leaving a story behind for the next human reader.
___
### 🧠 Flashcards

What is a literal?
?|?
A hardcoded value written directly in the source code. 

---

What makes string literals different from other types of literals in C++?  
?|?
 String literals are `const` objects created at program start and guaranteed to exist for the program’s lifetime.

---

Do string literals in C++ behave like primitive data types?  
?|?
No — they behave more like fixed `const` objects and are linked to C-style string handling.

#flashcards 