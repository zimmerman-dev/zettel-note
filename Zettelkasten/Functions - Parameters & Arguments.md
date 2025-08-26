#### 📝 Note: Functions - Parameters & Arguments 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚10:58 pm  📆 Mon Aug 11
 🔗 **Related Concepts**: #note #cpp [[Functions - Overview]] , [[Data Types]], [[Functions - Passing Arrays & Vectors]], [[Functions - User-defined]]
___
### 🥅 Function Parameters
Functions can accept **input values** when they're called. These values let the function do its job using real data.
#### ✅ Terminology
- **Arguments** — the actual values passed when calling a function
- **Parameters** — the placeholders used in the function definition

> The number, order, and types of arguments must match the parameters.
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

### 📦 Pass-by-Value (Default in C++)
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
### 🔁 Pass-by-Reference
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
### 🔍 Let’s Clarify
 🧵🌀 The **Multiverse Model** for Functions

- `main()` is **Universe A**
- A function like `modify()` is **Universe B**
###### 🔁 Pass-by-Value: _Courier between worlds_
- You send **a clone** of the variable through a one-way wormhole into Universe B.
- That clone lives and dies _inside_ that universe.
- Universe A’s original? Unchanged, untouched, unaware.
- Think of it like: “We sent a copy of our ambassador, not the real one.”
###### 🔗 Pass-by-Reference: _Shared portal between worlds_
- You open a **rift** between Universe A and B.
- Universe B reaches _through the portal_ to work directly on a variable in A.
- They’re not cloning, they’re meddling.
- Changes in Universe B _echo immediately_ in Universe A.
#### 🏷️ Formal vs Actual Parameters
- **Formal parameters** — declared in the function header  
    → `int addition(int a, int b)`
- **Actual parameters** — the arguments passed in the function call  
    → `addition(1, 2)`

See: [[Functions - Scope]]