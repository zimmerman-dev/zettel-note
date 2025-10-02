 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚6:05 pm  📆 Mon Sep 22
 🔗 **Related Concepts**: #note #cpp
___
## 📝 Note: Assignment & Initialization
In [[Statements and Expressions]], we laid a surface-level foundation on what assignment is, and we’ve alluded to initialization in different parts of this notebook. In this note, we’ll dive deeper into both concepts so we can connect them with fundamentals of memory management down the road.

Before going further, check out:  
[[Mixed Expressions & Type Conversions & Promotion]] and [[Introduction to Type Conversion and static_cast]].
___
### Assignment vs Initialization

- **Assignment**: After a variable is defined, give it a value.  
```cpp
int x; // Definition
x = 4; // Assignment (copy-assignment)
```

- **Initialization**: Give a variable its first value at the time of definition.  
```cpp
int x = 4; // Initialization
```

⚠️ Note: In C++, `=` is the assignment operator. For equality comparison, use `==` (see [[Operators - Relational & Logical]]).
___
### Forms of Initialization
C++ provides several forms of initialization. They look similar, but differ in behavior, conversions allowed, and type-safety.
```cpp
int a;     // Default-initialization
int b = 5; // Copy-initialization
int c(6);  // Direct-initialization
int d{7};  // Brace (direct-list) initialization
int e{};   // Value-initialization
```
--- start-multi-column: ID_msxs
```column-settings
Number of Columns: 2
Largest Column: Standard
Column Spacing: 3px
Border: off
Overflow: Hidden
```
#### Default-initialization
```cpp
int a; // Default-initialized
```
Leaves the variable with an indeterminate value (garbage). Not recommended for fundamental types.

--- column-break ---
#### Copy-initialization
```cpp
std::string name = "Tim";
```
Steps:  
1. `"Tim"` implicitly converts to a temporary `std::string`.  
2. Temporary is copied/moved into `name`.  
3. Temporary is destroyed.  

Allows implicit conversions, which can introduce subtle errors.

--- end-multi-column
___
--- start-multi-column: ID_ygnq
```column-settings
Number of Columns: 3
Largest Column: Center
Column Spacing: 3px
Border: off
Overflow: Hidden
```
#### Direct-initialization
```cpp
std::string name("Tim");
```
Constructs the object directly with the given argument. No temporary involved.

--- column-break ---
#### Brace (Direct-list) Initialization
Introduced in C++11. Also called **brace** or **uniform initialization**.  
```cpp
int x{5};
std::vector<int> v{1, 2, 3};
```

Advantages:  
- Prevents narrowing conversions  
- Works uniformly across types (fundamental, arrays, structs, classes)  
- Reduces constructor ambiguity  

Example of narrowing prevention:  
```cpp
int value{4.5}; // ❌ Error: narrowing conversion
```

--- column-break ---
#### Value-initialization
```cpp
int e{};
```
Initializes to zero (zero-initialization) for fundamental types. For user-defined types, calls a suitable constructor.

--- end-multi-column
### Why So Many Forms?
Different initialization forms exist because they control:  
- Whether implicit conversions are allowed.  
- Whether narrowing is permitted.  
- Which constructor is chosen (explicit vs implicit).  

Brace initialization was designed to improve type-safety and consistency.
___
### `[[maybe_unused]]` (C++17)

Sometimes you need a variable in your codebase (constants, placeholders, project-wide values) that isn’t always used. Modern compilers will warn about this, and if “treat warnings as errors” is enabled, your build might fail.

C++17 introduced the `[[maybe_unused]]` attribute to mark these cases explicitly:
```cpp
[[maybe_unused]] double gravity { 9.8 };
[[maybe_unused]] int unusedCounter {};
```
This tells both the compiler _and other developers_ that the variable’s presence is intentional, even if it isn’t referenced.
___
### Best Practices

- Prefer **brace-initialization** or **value-initialization** for safety and clarity (per Stroustrup & Sutter, C++ Core Guidelines).  
- Avoid leaving variables uninitialized.  
- Use `[[maybe_unused]]` to silence unused-variable warnings when the variable is still meaningful to keep in code.
___
### 🧠 Flashcards
  
What is the difference between assignment and initialization in C++?  
?|?  
**Answer**  
**Initialization** happens _at the point of variable definition_, giving it its first value.  
**Assignment** happens _after_ a variable has been defined, updating its value.

---
 
Which of these is initialization and which is assignment?
`int x = 5; x = 10;`
?|?  
`int x = 5;` → **Initialization**  
`x = 10;` → **Assignment**

---
  
Why is copy initialization potentially less type-safe than brace initialization?  
?|?    
Copy initialization allows **implicit conversions** and **narrowing** (e.g. `double → int`), which can lead to silent data loss.  
Brace initialization forbids narrowing and is more strict.

---

Which form of initialization creates a temporary and then moves or copies it?
`std::string name = "Tim";`
?|?  
**Copy initialization.**  
A temporary `std::string` is created from `"Tim"`, then moved (or copied) into `name`.

---


Which form of initialization constructs the object directly with no temporary?
`std::string name("Tim");`
?|?   
**Direct initialization.**  
The object is constructed in-place with the argument `"Tim"`.

---

What is brace initialization, and why is it called "uniform"?  
?|?  
Brace initialization uses `{}` to initialize variables. It’s called “uniform” because the syntax works across all types (fundamental, arrays, structs, classes) and reduces ambiguity.

---

What happens when you try to use brace initialization with a narrowing conversion?
`int x{4.5};`
?|?   
**Compilation fails.**  
Brace initialization forbids narrowing conversions to prevent silent truncation or data loss.

---

Which form of initialization is safest for preventing unintended type conversions?  
?|?  
**Brace initialization** — it disallows narrowing and forces explicitness, making it the safest choice for type safety.


#flashcards