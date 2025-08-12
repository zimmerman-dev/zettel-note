#### 📝 Note: Functions - Prototypes 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚11:01 pm  📆 Mon Aug 11
 🔗 **Related Concepts**: #note #cpp [[Functions - Overview]] , [[Functions - User-defined]] , [[Functions - Anatomy]] , [[Functions - Parameters & Arguments]] , [[Functions - Default Arguments]] , [[C++ Syntax Reference]] , [[Preprocessor Directives(STUB)]]
___
#### 📝 Note: Functions - Prototypes 
♻️ (*MinGW, Windows11, Codelite*)   
⌚11:01 pm  📆 Mon Aug 11  
🔗 **Related Concepts**: #note #cpp [[Functions - Overview]] , [[Functions - User-defined]] , [[Functions - Anatomy]] , [[Functions - Parameters & Arguments]] , [[Functions - Default Arguments]] , [[C++ Syntax Reference]] , [[Preprocessor Directives(STUB)]] , [[CMake]]
___
### 🤖 Function Prototypes
In small programs, it’s fine to define your functions before calling them. But in larger programs, this isn’t always practical — especially when functions are organized across multiple files.

A **function prototype** (also called a *forward declaration*) tells the compiler **what a function looks like** — its return type, name, and parameters — **without providing the full definition yet**.

Prototypes are typically placed at the **top of the file**, or in **header files** (`.h`) for reuse across multiple source files.

```cpp
#include <iostream>

void greet();  // Function prototype

int main() {
    greet();    // Function call
    return 0;
}

void greet() {  // Function definition (can come later)
    std::cout << "Hello";
}
```
#### 🧠 Key Points
- The prototype must match the function definition **exactly** — same return type, name, and parameter types.
- If the prototype declares no parameters, you can’t pass arguments when calling the function.
- A function can only have **one prototype** in a given scope.
- The order of prototypes in your file **doesn’t matter** — the compiler just needs to see them before the function is called.
- Default parameter values should be given **only** in the declaration, not in both places.

---
### 📢 Forward Declarations
A **forward declaration** tells the compiler that a function exists before its actual definition appears in the code.  
In C++, a **function prototype** is itself a type of forward declaration.

```cpp
// Forward declaration
int add(int a, int b);

int main() {
    int sum = add(3, 4);  // This works because the compiler already knows about `add`
    std::cout << sum;
}

// Function definition
int add(int a, int b) {
    return a + b;
}
```

---
### 📂 Forward Declarations Across Multiple Files
Forward declarations become especially important when your program spans **multiple files**.  
In this setup, we typically place declarations in **header files** (`.h`) and definitions in **source files** (`.cpp`).
#### Example Project Structure
```bash
project/
├── CMakeLists.txt
├── src/
│   ├── main.cpp
│   ├── add.cpp
│   └── add.h
```
> See: [[CMake]] for more on toolchain information.
#### **add.h** — Header File (Declaration)
```cpp
#pragma once  // Prevents multiple inclusions
int add(int a, int b); // Forward declaration
```
#### **add.cpp** — Source File (Definition)
```cpp
#include "add.h"

int add(int a, int b) {
    return a + b;
}
```
#### **main.cpp** — Using the Function
```cpp
#include <iostream>
#include "add.h"  // Brings in the forward declaration

int main() {
    std::cout << add(5, 7) << "\n";
}
```
> See: [[Preprocessor Directives(STUB)]] for more details on `#include` and `#pragma once`.

---

*See also: [[Functions - Default Arguments]] for more function-related details.*

