#### 📝 Note: Functions - Parameters & Arguments 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚10:58 pm  📆 Mon Aug 11
 🔗 **Related Concepts**: #note #cpp [[Functions - Overview]] , [[Functions - Anatomy]] , [[Functions - Default Arguments]] , [[Functions - Scope]] , [[C++ Syntax Reference]] , [[Data Types]]
___
### 🥅 Function Parameters
Functions can accept **input values** when they're called. These values let the function do its job using real data.
#### ✅ Terminology
- **Arguments** — the actual values passed when calling a function
- **Parameters** — the placeholders used in the function definition

> The number, order, and types of arguments must match the parameters.
##### Example:
```cpp
int main() {
    int result {};
    result = addition(1, 2);  // Call — 1 and 2 are *arguments*
    return 0;
}

int addition(int a, int b) {  // Definition — a and b are *parameters*
    return a + b;
}
```
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
#### 🏷️ Formal vs Actual Parameters
- **Formal parameters** — declared in the function header  
    → `int addition(int a, int b)`
- **Actual parameters** — the arguments passed in the function call  
    → `addition(1, 2)`

See: [[Functions - Scope]]