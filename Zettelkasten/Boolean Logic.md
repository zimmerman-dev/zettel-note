#### 📝 Note: Boolean Logic 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚9:27 pm  📆 Mon Jul 28
 🔗 **Related Concepts**: [[Control Flow]] , [[Statements and Expressions]] , [[Conditionals]] , [[Loops]] , [[C++ Syntax Reference]]
___
### ✅ What is Boolean Logic?
- Named after **George Boole**, based on true/false values.
- In C++, `bool` is a built-in type:  
  - `true` → 1  
  - `false` → 0  
### ✅ Boolean Operators (Logical)
- `&&` → Logical AND (true if **both** conditions are true)  
- `||` → Logical OR (true if **at least one** condition is true)  
- `!`  → Logical NOT (inverts true/false)  
### ✅ Relational Operators
- `==` → Equal to  
- `!=` → Not equal to  
- `<`, `>`, `<=`, `>=` → Comparisons that also return `bool`

### ✅ Short-Circuit Evaluation
- **Logical operators (`&&` and `||`) evaluate from left to right**.  
- Evaluation **stops** as soon as the result is determined:
  - `A && B` → if `A` is **false**, `B` is not evaluated.  
  - `A || B` → if `A` is **true**, `B` is not evaluated.  

#### 🔹 **Why this matters**
- **Prevents errors**:
  ```cpp
  if (x != 0 && (10 / x > 2)) { ... } // avoids division by zero
  ```
- **Improves performance** (skips unnecessary checks).  
- **Controls side effects** (the skipped expression never runs).

---

### ✅ Using `boolalpha`
```cpp
std::cout << std::boolalpha << (5 > 3); // prints true
```

---

### ✅ Conditional Expressions
- `if`, `while`, `for`, and the ternary `?:` all rely on boolean results.  
- Any non-zero value in a condition is treated as `true`.

---

### ✅ Examples
```cpp
bool isAdult = (age >= 18);
if (isAdult && hasID) {
    std::cout << "Access granted\n";
}