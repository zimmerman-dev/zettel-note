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
In C++, you can also pass arguments **by reference** using the `&` symbol in the parameter list. You can write it like this: `int& x`, `int & x`, or even `int &x`, but most common is `int& x`. What it means is:
- The function receives a **reference** to the original variable, not a copy.
- Any changes made to the parameter affect the original.
```cpp
void num(int& x) {
	x += 1;
}

int main() {
	int x {4};
	num(x);
	std::cout << x;   // Ouput 5 becuase value is modified by the num function
	return 0;
}
```
#### 🏷️ Formal vs Actual Parameters
- **Formal parameters** — declared in the function header  
    → `int addition(int a, int b)`
- **Actual parameters** — the arguments passed in the function call  
    → `addition(1, 2)`

See: [[Functions - Scope]]