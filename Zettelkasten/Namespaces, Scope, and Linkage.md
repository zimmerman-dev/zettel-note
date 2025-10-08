 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚3:51 am  📆 Sat Aug 30
 🔗 **Related Concepts**: #note #cpp [[Multi-File Programs]] [[Preprocessor Directives]] 
___
## 📝 Note: Namespaces, Scope, and Linkage
Before diving into namespaces, let’s establish the basics of **scope** and **blocks**.

A **compound statement** (or block statement) is a group of zero or more statements enclosed in `{}` that the compiler treats as a single unit. It also defines a **new scope region** — a boundary that limits where identifiers (like variables or functions) are visible.
___
### 🔹 Blocks and Nesting
There are three key things to know about a block:
- Blocks begin and end with curly braces `{}`.
- Blocks do **not** end with semicolons.
- Blocks can be nested within other blocks, forming **nested scopes**.

```cpp
int main() {
  // This is the outermost block (main function scope)
  if (condition) {
    // Nested block (inside if-statement)
    if (anotherCondition) {
      // Block nested inside another block
    }
  }
}
```
**Nesting Level** (or **Nesting Depth**) describes how deep blocks are nested. In the example above, the deepest level is 2 (not counting the main function block itself).
___
### 🔹 Scope Basics
A **scope** is a region of a program where a name (identifier) is valid and unique. Identifiers can be reused **in different scopes**, but must be unique **within the same scope**. The most common kind of scope is **block scope**, where a variable or function is only visible inside the block it was defined in.

As programs grow, **naming collisions** become more likely, which is why understanding scopes — and how to isolate them — becomes crucial.

Types of scope include:
- Function scope    
- Class scope    
- Block scope    
- **Namespace scope**    
- **Global scope**    

> 🔜 We’ll explore **duration** (how long objects live) and **linkage** (cross-file visibility) in later sections of Chapter 7.
___
### 🔹 Namespaces
A **namespace** is a named scope region used to organize identifiers into groups, especially to **avoid naming conflicts** across large programs.
#### Key Concepts
- Identifiers in different namespaces are treated as distinct, even if their names are identical.
- You can define variables, functions, and types in a namespace.  
- You **cannot** write executable statements directly in a namespace, only declarations and definitions.

```cpp
namespace foo {
    void myFunction(int x); // OK
}

namespace bar {
    void myFunction(int x); // OK — no conflict
}
```
To call one of these functions, use the **scope resolution operator `::`**:
```cpp
int main() {
    foo::myFunction(5);  // Calls foo's version
    bar::myFunction(10); // Calls bar's version
}
```
___
### 🔹 Naming Collisions
A naming collision occurs when two identifiers with the same name exist in a scope where they cannot be disambiguated. These errors are typically caught by the linker, not the compiler.

```cpp
// file1.cpp
void myFunction(int x) {
	std::cout << x;
}

// file2.cpp
void myFunction(int x) {
	std::cout << x + 5;
}
```
- ✅ Both files **compile** successfully.  
- ❌ But during **linking**, the linker sees **two functions with the same signature** in the global scope.  
- Even if `myFunction()` is never used, the linker still throws a **multiple definition** error. 

See also: [[Multi-File Programs]]
___
### 🔹 The Global Namespace
Any identifier **not declared inside a class, function, or namespace** belongs to the **global namespace**.
#### Key Points
1. Global names are visible from their point of declaration to the end of the file.
2. You _can_ define global variables — but it’s strongly discouraged.
3. The global scope is **always available**, and is the fallback when no namespace is specified.
___
### 🔹 The `std` Namespace & Scope Resolution Operator `::`
Originally, C++ put all standard library identifiers in the **global namespace**. But this caused frequent conflicts with user-defined names. The solution: move all standard library identifiers into the **`std` namespace**.

The `::` operator accesses names inside a namespace.
```cpp
#include <iostream>

int main() {
    std::cout << "Hello, world!\n"; // std::cout lives in the std namespace
}
```
___
### 🔹 Why You Should Avoid `using namespace std`
Although valid, `using namespace std;` is **discouraged in production code**.
#### Problems it creates:
- It **reintroduces the risk** of naming collisions — the very issue `std` solves.
- It makes code **less clear**, because you can’t tell where names are coming from.

✅ Prefer **explicit use** of `std::` for clarity and safety.
___
### 🔹 Variable Scope Recap
Before we get into linkage, let's recap.  Refer to [[Functions - Scope, Lifetime, and Temporaries]] for a deeper view into local and global variables.
--- start-multi-column: ID_3s3c
```column-settings
Number of Columns: 2
Largest Column: Standard
Column Spacing: 3px
Border: off
```
#### Local Variables
Local variables have block scope, meaning the variable's scope spans the block that it was defined in, inclusively.
```cpp
void foo(int a) { // a enters scope here

  int b{a}; // b enters scope here

} // a and b go out of scope here
```

Variables should always be defined in the narrowest possible scope. If a variable is only used within a nested block, define it inside that block.

--- column-break ---
#### Global Variables
In C++, variables declared outside of a function are called **Global variables**. By convention, global variables are declared at the top of a file, underneath the includes, in the global namespace. Variables declared in a user-defined namespace are also considered global scope.
```cpp
#include <iostream>
int x{1};

int main() {
  // ...
  return 0;
}
```
Since global variables are created when the program starts, and persist until the end of the program, it is said to have **static duration**.

For the most part, global variable's should be used sparingly unless it's a constant.

--- end-multi-column
___
### 🔹 Linkage
At first, **scope** and **linkage** seem very similar; however, where **scope** controls where in the current file a name is visible, **linkage** controls whether that name can be seen across files.
#### What is *linkage*?
To expand on our definition, linkage determines **whether a name** (variable or function) refers to the **same entity** when used across **multiple files**. In other words:
- Does this "name" have **internal linkage** (only visible in one file)?
- Does it have **external linkage** (can be shared across multiple files)?
- Or does it have **no linkage** (can only be used within its own scope, and cannot be accessed elsewhere)?
#### No Linkage
The variable **only exists inside its own scope; cannot be accessed elsewhere**.
Applies to: **Local Variables**.
- Cannot be linked to from other files.
- Doesn't persist across translation units (source files).
```cpp
void foo() {
  int x{42}; // No linkage (x only exists within foo)
}
```

Local variables like these have **no linkage** because they only exist within their own scope.  In contrast, **internal** and **external linkage** control how names behave at file and program level.
___
#### Internal Linkage
The name **can be used throughout the file, but not in other files**.
Applies to:
- `const` variables at global scope
- Anything marked `static` at global scope ( we will return to this below)
Compiler keeps the name local to this translation unit.
```cpp
// #include ...
static int counter{0};
const int kPi{3.14159};
// int main()
```
##### `static`
If the variable is constant, `static` is unnecessary. In general, if you need a global variable, make it a constant instead. Even though `static` variables are hidden from other files, they remain mutable within their file, which can make them error-prone.
___
#### External Linkage
The name refers to the **same entity across multiple files**.
Applies to:
- Non-const global variables (by default)     
- Functions (by default)
- Anything declared with `extern` (we will return to this below)
Used in **multi-file programs**
```cpp
extern int g_var; // External linkage

void doSomething() { // Also external linkage
    std::cout << g_var;
}
```
##### `extern`
The `extern` keyword behaves like a forward declaration for a variable. It tells the compiler that the variable being declared already exists in another translation unit. No new storage is created—this declaration simply refers to the existing variable.

Example:
```cpp
// file 1
int counter{43};

// file 2
extern int counter;
std::cout << counter << '\n';
```
> Output will be 43 even though `counter` was defined and initialized in another file.
___
### 📌 Key Terms and Concepts
- A **block** is a `{}`-enclosed region that introduces a new scope  
- A **scope** limits the visibility of names; identifiers must be unique within a scope  
- **Namespaces** allow grouping of identifiers and prevent naming collisions  
- The **global namespace** is always available but should be used with caution  
- The **`std` namespace** contains all standard library names; avoid importing it wholesale  
- **Naming collisions** often occur during the linking phase, not compilation  
- **Linkage** controls whether a name can be shared across files  
- Use `const` (or `constexpr`) for safe globals  
- Use `static` for file-local globals that must remain hidden  
- Use `extern` when multiple files need to refer to the same variable or constant
___
### 🧠 Flashcards

What is a compound statement (or block) in C++? 
?|? 
A group of zero or more statements enclosed in `{}` that the compiler treats as a single unit; it also defines a new scope region.

---
What does the term “nesting depth” describe? 
?|? 
How many levels of nested blocks exist within one another in a program.

---
What is scope? 
?|? 
The region of a program where a name (identifier) is visible and valid.

---
What is a namespace in C++? 
?|? 
A named scope region used to organize identifiers and prevent naming collisions across large programs.

---
What is the purpose of the scope resolution operator `::`? 
?|? 
It accesses names that live inside a specific namespace or global scope (e.g., `std::cout`).

---
What is the global namespace? 
?|? 
The default, top-level scope where names declared outside any function, class, or namespace reside.

---
What is linkage? 
?|? 
A property that determines whether a name refers to the same entity across multiple source files.

---
What is internal linkage? 
?|? 
Linkage where a name is visible only within its own translation unit (e.g., `static` or `const` globals).

---
What is external linkage? 
?|? 
Linkage where a name refers to the same entity across multiple translation units (e.g., non-const globals, functions, or variables declared with `extern`).

---
What does the `extern` keyword do? 
?|? 
Declares that a variable is defined in a


#flashcards 