 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚3:51 am  📆 Sat Aug 30
 🔗 **Related Concepts**: #note #cpp [[Multi-File Programs]] [[Preprocessor Directives]] 
___
## 📝 Note: Namespaces
###  🔹 Naming Collisions
When two or more **identical identifiers** exist in a program and **cannot be disambiguated**, a _naming collision_ (or naming conflict) occurs.
####  Key Points
- All C++ identifiers must be **unique within their scope**.
- Collisions are usually detected by the **linker**, not the compiler.
- This can happen **even if the duplicated name is never used**.
####  Example (across multiple files):
```cpp
void myFunction(int x) {
	std::cout << x;
}
```

```cpp
void myFunction(int x) {
	std::cout << x + 5;
}
```

>- ✅ Each file **compiles** fine.
>- ❌ But during linking, the linker sees **two `myFunction()`s with the same signature** in the global scope.
>- Even if `myFunction()` is never called, the linker **still throws an error** because both definitions exist.

See also: [[Multi-File Programs]]
___
### 🔹 Scope Regions
A **scope region** defines a boundary within which names must be unique.  
You can reuse names **safely in different scopes**, but **never within the same one**.
####  Key Points
- As your program grows, the chance of collision increases.
- Scope types: function scope, class scope, block scope, **namespace scope**, and **global scope**.
___
### 🔹 Namespaces
A **namespace** is a scope region that helps **group identifiers** to avoid name conflicts.
####  Key Concepts
- Names inside different namespaces are treated as **distinct**, even if identical.
- You can define **functions, variables, and types** in a namespace.
- You **cannot write executable statements** directly inside a namespace (only declarations or definitions).
####  Example:
```cpp
namespace foo {
    void myFunction(int x); // okay
}
namespace bar {
    void myFunction(int x); // okay — no conflict
}
```
___
### 🔹 The Global Namespace
Any identifier **not declared inside a function, class, or namespace** belongs to the **global namespace** (aka global scope).
####  Key Points
1. Global names are visible from their point of declaration to the end of the file.
2. You _can_ define global variables—but it’s **discouraged**. (We’ll revisit this later.)
### 🔹 The `std` namespace
Originally, all standard library identifiers lived in the **global namespace**, which led to **collisions with user-defined names**.  
To solve this, C++ moved all standard identifiers into a dedicated **`std` namespace**.
####  Using `std::` with the Scope Resolution Operator `::`
- The `::` operator accesses names inside a namespace.
- `std::cout` tells the compiler to use `cout` from the `std` namespace.
```cpp
#include <iostream>

int main() {
	std::cout << "Hello, world! \n";
}
```
### 🔹 Avoid `using namespace std`
Although you _can_ use the `using namespace std;` directive, it is bad practice in real, production code.
####  Why it’s discouraged:
- It reintroduces the risk of **naming collisions**—the exact problem `std` was designed to prevent.
- You lose clarity about **where identifiers come from**.

Prefer **explicit usage** of `std::` to avoid surprises.
___
### 📌 Summary of Key Concepts
- **Naming collisions** happen when two identifiers in the same scope can't be disambiguated.
- **Namespaces** create isolated scope regions to prevent these collisions.
- **Scope regions** allow identifiers with the same name to coexist as long as they're in different scopes.
- The **global namespace** is the default if no namespace is provided.
- The **`std` namespace** holds standard library identifiers—don’t use `using namespace std;` in real projects.
---
### 🧠 Flashcards


