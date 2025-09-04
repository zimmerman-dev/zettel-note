 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚10:58 pm  📆 Mon Aug 11
 🔗 **Related Concepts**: #note #cpp [[Functions - Overview]] , [[Data Types]], [[Functions - Passing Arrays & Vectors]], [[Functions - User-defined]]
___
## 📝 Note: Functions - Parameters & Arguments
- A **function parameter** is a variable declared in the function header, specifically within the _parameter list `()`_. It allows the function to **receive data from the caller** so it has values to operate on.
### 🔹 TL;DR – Parameters vs. Arguments
- **Parameter** → the variable in the function **that receives** data
- **Argument** → the actual data **being sent** to the function
- **Direction**: caller → function
- **Location**:
	- Parameters are in the **function definition**
	- Arguments are in the **function call**
##### Example:
```cpp
#include <iostream>
// Forward Declaration: tells compiler about addition before we use it
int addition(int a, int b);

int main() {
    int result {};
    result = addition(1, 2);  // Call — 1 and 2 are *arguments*
    return 0;
}

int addition(int a, int b) {  // Definition — a and b are *parameters*
    return a + b;
}
```
> Function prototype must appear before use, or a forward declaration is needed

### 🔹 How They Work Together
When a function is called, all of the parameters of the function are created as variables, and the value of each of the arguments is **copied** into the matching parameter (using copy initialization). Function parameters that utilize pass by value are called **value parameters**.
### 🔹 Pass-by-Value (Default in C++)
When you pass arguments to a function in C++, they are passed **by value** — this means:
- A **copy** of the argument is made.
- The function works with the copy.
- The original argument remains **unchanged**.
```cpp
void change(int x) {
    x = 100;
}

int main() {
    int a = 10;
    change(a);
    std::cout << a; // Still prints 10
}
```
### 🔹 Pass-by-Reference
##### Sometimes we want a function to **modify the actual argument**, not just a copy.
- To do this, we need the **location** (memory address) of the variable, not its value.
- This technique is called **pass-by-reference**, and it uses the `&` symbol in the parameter list.
##### You can write **reference parameters** like this:
- `int& x`
- `int & x`
- `int &x`  
  → All are valid, but `int& x` is the most commonly seen style.
##### What this means:
- The function receives a **reference** to the *original* variable.
- It can access and modify the value *in memory*.
- Any changes to the parameter **directly affect the caller's variable**.
```cpp
void num(int& x) {
	x += 1;
}

int main() {
	int x {4};
	num(x);
	std::cout << x;   // Ouput: 5 (because the original was modified)
	return 0;
}
```
### 🔹 Let’s Clarify
 🧵🌀 The **Multiverse Model** for Functions

- `main()` is **Universe A**
- A function like `modify()` is **Universe B**
######  Pass-by-Value: _Courier between worlds_
- You send **a clone** of the variable through a one-way wormhole into Universe B.
- That clone lives and dies _inside_ that universe.
- Universe A’s original? Unchanged, untouched, unaware.
- Think of it like: “We sent a copy of our ambassador, not the real one.”
######  Pass-by-Reference: _Shared portal between worlds_
- You open a **rift** between Universe A and B.
- Universe B reaches _through the portal_ to work directly on a variable in A.
- They’re not cloning, they’re meddling.
- Changes in Universe B _echo immediately_ in Universe A.
####  Formal vs Actual Parameters
- **Formal parameters** — declared in the function header  
    → `int addition(int a, int b)`
- **Actual parameters** — the arguments passed in the function call  
    → `addition(1, 2)`

See: [[Functions - Scope, Lifetime, and Temporaries]]
___
### 🧠 Flashcards

**Q:** What is the difference between a parameter and an argument?
?|?
**A:**
- A **parameter** is the variable declared in the function **definition** to receive data.
- An **argument** is the actual value passed in the function **call**.
<!--SR:!2025-09-02,4,270-->

**Q:** In this function header, which are the parameters?
```cpp
int multiply(int a, int b);
```
?|?
**A:** `int a` and `int b` are the parameters — they are defined in the parameter list.
<!--SR:!2025-09-02,4,270-->

**Q:** What is the default method of passing arguments in C++? |?| **A:** **Pass-by-value** — arguments are **copied** into the function’s parameters.
<!--SR:!2025-09-02,4,270-->

**Q:** What symbol is used to indicate a pass-by-reference parameter in C++? |?| **A:** The `&` symbol (ampersand).
<!--SR:!2025-09-02,4,270-->

**Q:** What is the output of the following code?
```cpp
void change(int x) { x = 100; }
int main() {
    int a = 10;
    change(a);
    std::cout << a;
}
```
?|?
**A:** `10` — because `a` was passed by value and not modified.
<!--SR:!2025-09-02,4,270-->

**Q:** What does this code do?
```cpp
void update(int& x) { x += 1; }
int main() {
    int y = 4;
    update(y);
    std::cout << y;
}
```
?|?
**A:** Outputs `5` — `y` was passed **by reference**, so the original was modified.
<!--SR:!2025-09-02,4,270--> 

**Q:** What do we call parameters declared in the function header? |?| **A:** **Formal parameters**
<!--SR:!2025-08-30,1,230-->

**Q:** What do we call the values passed in the function call? |?| **A:** **Actual parameters** (also known as arguments)
<!--SR:!2025-09-01,3,250-->

#flashcards 


____
####  Functions - Parameters & Arguments: *Subsection* 
 ♻️ *subsection*   
 ⌚5:35 pm  📆 Tue Sep 2
 🔗 **Related Concepts**: #note
___
## Function Input Design: Pass-by-Value vs Pass-by-Reference
When designing functions that collect **user input** or **fill existing variables**, the choice between **pass-by-value** and **pass-by-reference** has direct consequences on **clarity, performance, and memory usage**.

This note captures core design reasoning and best practices for user input functions in C++.
### 🔹 Two Common Styles
### 🔹 Pass-by-Reference (Preferred for Input)

```cpp
void userInput(int& out) { std::cin >> out; }
void userInput(std::string& out) { std::getline(std::cin >> std::ws, out); }
```

-  Clearly communicates mutation of an existing variable
-  No temporary objects or extra allocations
-  Enables overloading (based on parameter type)
-  Ideal for `std::string`, `std::vector`, or large objects

**Usage:**

```cpp
int age;
userInput(age);

std::string name;
userInput(name);
```

---

### 🔹 Return-by-Value (Valid, but can be less efficient)

```cpp
int userInput() {
    int val {};
    std::cin >> val;
    return val;
}
```

-  Clean syntax for simple types (`int`, `char`, etc.)
-  Creates a **temporary object**, which is then **copied or moved**
- ❌ Cannot overload on return type alone (C++ limitation)
- ⚠️ Can be less performant with non-trivial return types (e.g., `std::string`, `std::vector`)

**Usage:**

```cpp
int age = userInput();
```

---

### 🔹 Design Rule: Avoid Unnecessary Temporaries

> “If the function's job is to **fill a variable**, pass it by reference.  
> If its job is to **produce a value**, return it.”

Why pass-by-reference can be better:
-  Less abstraction—directly modifies caller's memory
-  Avoids heap allocations / move constructors
-  Explicit about **intent** and **ownership**
-  Critical in embedded or performance-conscious environments
---