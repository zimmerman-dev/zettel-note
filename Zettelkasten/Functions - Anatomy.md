#### 📝 Note: Functions - Anatomy 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚10:56 pm  📆 Mon Aug 11
 🔗 **Related Concepts**: #note #cpp [[Functions - Overview]] , [[Functions - Parameters & Arguments]], [[Functions - User-defined]]
___
### 🧱 Function Anatomy
A **function definition** provides the **actual implementation** of what a function does when it's called. It includes:
- **Return type** — the type of value the function gives back (`int`, `void`, etc.)
- **Function name** — how the function is called (see [[Variables and Objects]] for naming rules)
- **Parameters** — the inputs it receives (not always required)
- **Body** — the actual statements (inside `{}`)

```cpp
return_type function_name(parameter_type parameter_name, ...) {
    // statements
    return value; // only if return_type is not void
}
```

---
### 🔁 What Does "Return" Mean?
Returning a value means sending **a result back** to wherever the function was called. It's not the same as printing something on screen.

```cpp
int add(int x, int y) {
    return x + y;
}
```
- The function **does the work**
- Then it **returns** a value to use elsewhere:
```cpp
int result = add(2, 3);
std::cout << result; // prints 5
```
###  🏷️ C++ Return Types 
- `int` - Returns an integer 
- `double` - Returns a floating point number
- `bool` - Returns a true or false
- `char` - Returns a single character
- `std::string` - Returns a string
- `void` - The No Return Value
#### 🧤 Special Case: `void`
If a function doesn’t return a value, use `void`:
```cpp
void greet() {
    std::cout << "Hello!\n";
    return; // optional
}
```
- You can still use `return;` to exit early
- But **you cannot return a value**
### 🧠 Pro Tips
1. **Return Type Must Match**  
    If your function promises to return `int`, it must do so.  
    Otherwise, the compiler will throw an error.

2. **Function Order Matters**  
    The compiler must know about a function **before** it’s called.
    - Either define it before `main()`,
    - Or use a **function prototype**.

3. **Multiple Returns**  
    You _can_ use multiple `return` statements, but keep it readable.
```cpp
int classify(int score) {
    if (score >= 90) return 1;
    if (score >= 75) return 2;
    return 3;
}
```

See: [[Functions - Parameters & Arguments]]