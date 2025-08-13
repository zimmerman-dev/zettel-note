#### 📝 Note: Functions - Overview 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚10:48 pm  📆 Mon Aug 11
 🔗 **Related Concepts**: #note #cpp [[Functions - Built-in]] , [[Functions - User-defined]] , [[Functions - Parameters & Arguments]] , [[Functions - Default Arguments]] , [[Functions - Prototypes]] , [[Functions - Anatomy]] , [[Functions - Scope]]
___
## 🧠 Functions — Why Use Them?
> *“Why not just write everything in `main()`?”*

As programs grow, writing everything in one block becomes messy and hard to manage. Functions solve this by introducing:

- **Organization** – Break complex programs into manageable parts.
- **Reusability** – Reuse logic without rewriting code.
- **Testability** – Simplify testing by isolating logic.
- **Extensibility** – Make changes in one place that affect many others.
- **Abstraction** – Focus on what a function does, not how.

---
### 🔹 What is a Function?
A function is a **named sequence of statements** that performs a specific task.

- May accept input (parameters)
- May return a value (via `return`)
- Enables modular, logical code structure

![[Function Structure.png]]

---
### 📚 Built-in vs. User-defined Functions

#### ✅ Built-in Functions
Provided by the language or standard library headers like `<iostream>`, `<cmath>`, `<algorithm>`, etc.

Example:
```cpp
std::cout << std::sqrt(16); // Uses built-in functions from <iostream> and <cmath>
```

See [[Functions - Built-in]].
#### 🛠️ User-defined Functions
Functions you write yourself to encapsulate logic specific to your program.

Example:
```cpp
int add(int x, int y) {
    return x + y;
}
```

See [[Functions - User-defined]].

---
### 📁 Function Notes Backlinks
- [[Functions - Overview]] (this note)
- [[Functions - Built-in]]
- [[Functions - User-defined]]
- [[Functions - Anatomy]]
- [[Functions - Parameters & Arguments]]
- [[Functions - Scope]]
- [[Functions - Prototypes]]
- [[Functions - Default Arguments]]
- [[Functions - Overloading]] 
- [[Functions - References & Pointers(STUB)]] *(planned)*
