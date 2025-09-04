 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚10:48 pm  📆 Mon Aug 11
 🔗 **Related Concepts**: #note #cpp [[Functions - Built-in]] , [[Functions - User-defined]] , [[Functions - Parameters & Arguments]] , [[Functions - Default Arguments]] , [[Functions - Prototypes]] , [[Functions - Anatomy]] , [[Functions - Scope, Lifetime, and Temporaries]] , [[Functions - Passing Arrays & Vectors]] , [[Functions - References & Pointers(STUB)]]
___
## 📝 Note: Functions - Overview
> *“Why not just write everything in `main()`?”*

As programs grow, writing everything in one block becomes messy and hard to manage. Functions solve this by introducing:

- **Organization** – Break complex programs into manageable parts.
- **Reusability** – Reuse logic without rewriting code.
- **Testability** – Simplify testing by isolating logic.
- **Extensibility** – Make changes in one place that affect many others.
- **Abstraction** – Focus on what a function does, not how.
---
### 🔹 What Do We Already Know?
- A function is a **named, reusable sequence of statements** designed to do a particular job.
- **main()**: A function where to program starts execution when it is run.
- We can create [[Functions - Built-in|our own functions]] and their are [[Functions - Built-in|built-in functions]].
- The function initiating the function call is the **caller**, and the function being called (executed) is called the **callee**
### 🔹 Built-in vs. User-defined Functions
####  User-defined Functions
Functions you write yourself to encapsulate logic specific to your program.
**Example**:
```cpp
int add(int x, int y) { // Function Header
    return x + y;       // Function Body
}
```

> **Function Header** tells the compiler about existence of the function. 
> **Function Body** tells the compiler what the function does.
> ___
####  Built-in Functions
Provided by the language or standard library headers like `<iostream>`, `<cmath>`, `<algorithm>`, etc.
**Example**:
```cpp
std::cout << std::sqrt(16); // Uses built-in functions from <iostream> and <cmath>
```
### 🔹 What's in a function?
![[Function Structure.png]]
In the image above, we see:
- the `returnType` in blue. 
- The functions identifier in red, `function_name`.
- The green parentheses contain the parameter list.
- And the orange is is body and return statement.

For more info on this: [[Functions - Anatomy]]
___
### 📌 Key Definitions


---
### 🧠 Flashcards
Q:
In a function definition, what are the curly braces and statements in-between called?
A:
The function body 

Q:
What is `main()` in a C++ program?
A:
`main()` is the **entry point** of the program — the function where execution begins.

Q:
 In the function diagram, what does the `returnType` represent?
A:  
The **type of value** the function sends back to the caller (e.g. `int`, `double`, `void`)

Q:
What part of a function executes its logic?
A:
The **function body**, which includes statements and the `return` line

Q:
 What part of a function is responsible for input?
A:
The **parameter list** inside the parentheses (e.g. `(int x, int y)`)

#flashcards 