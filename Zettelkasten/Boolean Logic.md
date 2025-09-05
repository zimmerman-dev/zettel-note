 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚9:27 pm  📆 Mon Jul 28
 🔗 **Related Concepts**: #note #cpp [[Literals & Operators]], [[Control Flow]], [[Fundamental Data Types]]
___
## 📝 Note: Boolean Logic
### 🔹 What is Boolean Logic?
- Named after **George Boole**, based on true/false values.
- In C++, `bool` is a built-in type:  
  - `true` → 1  
  - `false` → 0  
####  The "truthy-falsey" Caveat
- While it is true that `true` prints as `1` and `false` prints as `0` by default; under the hood, any non-zero scalar type, even negative numbers are "*truthy*" and treated as `true` in Boolean context.
- This concept is used everywhere but especially in `if`, `while`, `for`, ternary `?:`, etc.
### 🔹 Boolean Operators (Logical)
- `&&` → Logical AND (true if **both** conditions are true)  
- `||` → Logical OR (true if **at least one** condition is true)  
- `!`  → Logical NOT (inverts true/false)  
### 🔹 Boolean Operators (Relational)
- `==` → Equal to  
- `!=` → Not equal to  
- `<`, `>`, `<=`, `>=` → Comparisons that also return `bool`

---

This is why **non-boolean expressions** can still be used directly in conditions:
```cpp
if (x)   // true if x != 0
if (!x)  // true if x == 0
```
### 🔹 Short-Circuit Evaluation
- **Logical operators (`&&` and `||`) evaluate from left to right**.  
- Evaluation **stops** as soon as the result is determined:
  - `A && B` → if `A` is **false**, `B` is not evaluated.  
  - `A || B` → if `A` is **true**, `B` is not evaluated.  
####  **Why this matters**
- **Prevents errors**:
  ```cpp
  if (x != 0 && (10 / x > 2)) { ... } // avoids division by zero
  ```
- **Improves performance** (skips unnecessary checks).  
- **Controls side effects** (the skipped expression never runs). 
#### Truth Table

| **Type** | **Example Value** | **Boolean Result** | **Explanation**                     |
| -------- | ----------------- | ------------------ | ----------------------------------- |
| `bool`   | `true` / `false`  | `true` / `false`   | Stored directly as `1` or `0`       |
| `int`    | `0` / `42`        | `false` / `true`   | Zero = false; any non-zero = true   |
| `double` | `0.0` / `-3.14`   | `false` / `true`   | Same rule applies                   |
| `char`   | `'\0'` / `'A'`    | `false` / `true`   | Null char = false; any other = true |
| Pointers | `nullptr` / `&x`  | `false` / `true`   | Null = false; valid address = true  |
| Enums    | `0` / `RED=1`     | `false` / `true`   | Same rule — zero = false            |

---
### 🔹 Using `boolalpha`
```cpp
std::cout << (5 > 3);                     // prints 1 (true as numeric)
std::cout << std::boolalpha << (5 > 3);   // prints true (flag changes representation)
std::cout << std::noboolalpha << (5 > 3); // prints 1 again (reset to default)
```

- `std::boolalpha` (from the `<iostream>` header) is a **stream manipulator** that changes how Booleans are represented in output.
- When enabled, Booleans print as `true` or `false` instead of `1` or `0`.
- `std::noboolalpha` resets the stream back to the **default numeric representation**.
---
### 🔹 Conditional Expressions
- `if`, `while`, `for`, and the ternary `?:` all rely on Boolean results.  
- Any non-zero value in a condition is treated as `true`. (We can reconsider this as we learn more about implicit conversions later)

---
### 🔹 Examples
```cpp
bool isAdult = (age >= 18);
if (isAdult && hasID) {
    std::cout << "Access granted\n";
}
```
___
##  Boolean Logic Recap
Boolean logic in C++ deals with **true/false values** and **expressions** that evaluate to those values.
- In C++, `bool` is a built-in type.
- `true` → stored as `1`
- `false` → stored as `0`
- In conditions, **zero means false**, and **any non-zero scalar value means true**.
- Used everywhere: `if`, `while`, `for`, ternary `?:`, etc.
### 📌 Key Definitions
1. **Boolean Type (`bool`):** A primitive data type representing the logical states `true` (1) or `false` (0). Also an integral type.
2. **Boolean Logic:** A system of evaluating conditions based on `true` or `false` values.
3. **Logical Operators:** Combine or invert Boolean expressions, especially in compound expressions.
	1. `&&` - Logical AND operator --> `true` if both operands evaluate `true`
	2. `||`  -  Logical OR operator --> `true` if at least one operand evaluates `true`
	3.  `!` - Logical NOT operator --> inverts the `truth` value, e.g., `!true == false`
4. **Relational Operators**: These are binary operators used to compare two operands and determine the relationship between them`<`, `>`, `==`, `!=`, `<=`, and `>=`
5. **Short-Circuit Evaluation**: Using logical operators, the compiler skips the execution or evaluation of some sub-expression in a logical expression.
6. `std::boolalpha` vs `std::noboolalpha`: `std::boolalpha` is a stream manipulation device where in place of a bool numeric value, it prints either true or false. The `std::noboolalpha` resets that back to the numeric value 
7. **Truthy/Falsey**: This is an idiom used in C++ to describe how non-zero values are inherently "truthy" while zero values are "falsey".
8. **Conditional Expression**: Also known as a **ternary operator** is concise retranslation of an if/else 
	1. using the syntax: `condition ? expression : expression;
---
### 🧠 Flashcards

- In C++, what values evaluate to `false` in a boolean context?|||Only values equivalent to `0` — everything else is treated as `true`.

- What does the `&&` operator do?|||Logical AND — evaluates to `true` only if **both** operands are true. 

- What does the `||` operator do?|||Logical OR — evaluates to `true` if **at least one** operand is true. 

- What does the `!` operator do???|||Logical NOT — flips `true` to `false` and vice versa. 

- What does a *short-circuit evaluation* mean for `&&` and `||`?|||Short-circuit evaluation is a programming language feature that skips evaluating the rest of a logical expression (like && or ||) once the overall result is already determined. 

- What does `std::boolalpha` and `std::noboolalpha` mean? Explain the difference.||| `std::boolalpha` makes `std::cout` print true/false instead of 1/0. `std::noboolalpha` sets it back to the numeric representation of bool.  
#flashcards