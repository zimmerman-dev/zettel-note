#### 📝 Note: Functions - Built-in 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚5:03 pm  📆 Mon Aug 11
 🔗 **Related Concepts**: #note #cpp [[Functions - Overview]] , [[Standard Library(STUB)]] , [[Preprocessor Directives(STUB)]] , [[C++ Syntax Reference]] , [[cmath(STUB)]] , [[cstdlib(STUB)]] , [[cstring(STUB)]] , [[cctype(STUB)]]
___
## 🧰 Built-In Functions (C++)

C++ provides many libraries with **predefined functions**, which you can use by including their header files using the `#include` directive with angle brackets.

The **Standard Template Library (STL)** is a collection of such headers, offering a wide range of built-in functions and tools.  
- See [[Standard Library(STUB)]] for a general overview
### 🧠 What Is a Built-In Function?
- Provided by the **standard library** or, in rare cases, the **compiler itself**
- Typically require a header (e.g., `#include <iostream>`)
- Behave like user-defined functions:
  - Use parentheses
  - May take arguments
  - May return values
- Some are part of a **namespace**, such as `std::`
### 📦 How to Use Them
When writing a program, you often start with:

```cpp
#include <iostream>
#include <cmath>               
//--------------------Header-files-above-this-line------------------------//
int main() {
    std::cout << std::sqrt(25); // prints 5
}
```

- `#include` is a **preprocessor directive** that tells the compiler to load the correct header
- `25` is the **argument** passed to the function `std::sqrt`
- `std::` indicates this function lives in the **Standard namespace**
### 🧾 Header File Requirements
- Functions only work if the correct header is included
- C++ uses angle brackets for standard headers: `#include <cmath>`
- Some older C-style headers exist (`<stdio.h>`) but are rarely used in modern C++

> See [[Preprocessor]] for more on `#include`
### 🔍 Categories of Built-In Functions
#### 1. I/O Functions
- `std::cout`, `std::cin`, `std::getline`
- Found in `<iostream>`
#### 2. Math Functions
- `std::sqrt`, `std::pow`, `std::abs`
- Found in `<cmath>`
#### 3. String & Character Functions
- `std::toupper`, `std::tolower` (via `<cctype>`)
- `std::getline`, `.length()`, `.at()` (via `<string>`)
#### 4. Algorithm Functions (STL)
- `std::sort`, `std::find`, `std::count`
- Part of the STL — see [[Standard Library(STUB)]]
### ⚠️ Notes on Usage
- Built-in functions are **used**, not defined
- Common issues if a function isn’t working:
    - Missing `#include` directive
    - Forgetting to use the correct **namespace** (like `std::`)