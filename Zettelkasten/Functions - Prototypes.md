♻️ (*MinGW, Windows11, Codelite*)   
 ⌚11:01 pm  📆 Mon Aug 11
 🔗 **Related Concepts**: #note #cpp [[Functions - Overview]] , [[Functions - Overview]], [[Functions - User-defined]]
___
## 📝 Note: Functions - Prototypes 
### 🤖 Function Prototypes
In small programs, it’s fine to define your functions before calling them. But in larger programs, this isn’t always practical — especially when functions are organized across multiple files.

A **function prototype** (a type of *forward declaration*) is a declaration statement including the return type, function name, and parameter types to inform the compiler of the functions' existence before being defined.

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
A **forward declaration** is a declaration the informs the compiler of an identifier (like a function, class, or variable) before its **full definition** appears in the code.
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

> See: [[Preprocessor Directives]] for more details on `#include` and `#pragma once`.
>___

See also: [[Functions - Default Arguments]] for more function-related details.*
___
### 🧠 Flashcards

**Q1: What is a function prototype in C++?** |?| A: A function prototype tells the compiler about a function’s return type, name, and parameters without defining its body.

**Q2: What happens if you call a function before the compiler has seen its prototype or definition?** |?| A: The compiler will throw an error because it doesn’t know the function’s type signature.

**Q3: What does this program output and why?**
```cpp
#include <iostream>

int greet();  // Prototype

int main() {
    greet();
    return 0;
}

int greet() {
    std::cout << "Hello\n";
}
```
?|?
**A:** Outputs `Hello`, but may produce a warning: `greet()` is declared to return `int` but no `return` statement is given in the definition. This is undefined behavior.

**Q4: Identify the issue in this code snippet:**
```cpp
void sayHi(int name = 1);  // Prototype with default value

void sayHi(int name = 1) { // Definition also repeats default
    std::cout << name;
}
```
?|?
**A:** ❌ Invalid: Default parameter value should only appear in the **declaration**, not the **definition**. This causes a compiler error.

**Q5: Where are function prototypes typically placed in a program?** |?| A: At the top of the source file or inside header (`.h`) files when used across multiple source files.

**Q6: True or False: You can have multiple prototypes of the same function in the same scope.** |?| A: False — a function can only have one prototype per scope.

**Q7: What must match exactly between a prototype and a function definition?** |?| A: The return type, function name, and parameter types (order and type).

**Q8: Why are forward declarations important in multi-file programs?** |?| A: They allow functions defined in one `.cpp` file to be declared in a shared `.h` file and used in other `.cpp` files.

**Q9: What’s the difference between a forward declaration and a function prototype?** |?| A: In C++, a function prototype **is** a type of forward declaration — specifically one that declares a function’s interface.

**Q10: Where should default parameter values be specified: in the prototype or the definition?** |?| A: In the prototype/declaration only. Not in both.

#flashcards 