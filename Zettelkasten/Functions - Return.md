 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:28 pm  📆 Thu Aug 28
 🔗 **Related Concepts**: #note #cpp [[Functions - Overview]] [[Functions - Anatomy]] [[Functions - Prototypes]] [[Functions - Parameters & Arguments]]
___
## 📝 Note: Functions - Return
### 🔹 Returning a Value
- A **value-returning function** sends a single value back to the caller.
- Two key components:
    1. **Return type** → Declares the type of value being returned.
    2. **Return statement** → Uses `return <expression>;` to produce the value.
**Process:**
1. The expression after `return` is evaluated.
2. The result is **copied** back to the caller.
3. The function exits immediately after returning.

> This is called **return by value**.
>___
### 🔹 Ignoring Return Values
- The caller can choose to ignore the returned value.
- If unused, the value is simply discarded.
```cpp
int return7() { return 7; }

int main() {
    return7();  // Value ignored here
    return 0;
}
```
---
### 🔹 Reusing Return Values
If you need the value multiple times, store it in a variable:
```cpp
int value { return7() };
std::cout << value << '\n';
```
### 🔹 Single Return Value Limitation
- A function can only return **one value** directly.
- Workarounds (e.g., structs, references, tuples) are covered later.
---
### 🔹 Revisiting `main()` 
- `main()` is called by the OS at program start.
- When `main()` finishes, it **returns an integer** called a **status code**:
    - `0` → Program executed successfully.
	- Nonzero → Indicates an error (customizable).
```cpp
  int main() {
    return 0;  // Equivalent to EXIT_SUCCESS
}  
    ```

> `EXIT_SUCCESS` and `EXIT_FAILURE` are defined in `<cstdlib>` and covered later.
>___
### 🔹Void Functions
#### `void()`
- To tell the compiler that your function does **not** return a value to the caller, you use the return type `void`.
- This is called a **non-value returning function**.

**Example:**
```cpp

#include <iostream>

  

// void means the function does not return a value to the caller

void printHi()

{

std::cout << "Hi" << '\n';

  

return; // optional: control returns to the caller here

} // function would return here if no `return;` was given

```

> `void` functions don't need a `return` statement, but one can be used **without a value** to exit early.

> ⚠️ Best practice: *Avoid using `return;` unless early exit is needed.*

---
- `void` functions **cannot be used in expressions** that expect a value.
**Example:**

```cpp

#include <iostream>

  

void printHi()

{

std::cout << "Hi" << '\n';

}

  

int main()

{

printHi(); // ✅ okay: function runs, no value returned

std::cout << printHi(); // ❌ compile error: no value to output

  

return 0;

}

```
---

- Attempting to `return` a **value** from a `void` function results in a compile error.

```cpp

void badReturn() {

return 42; // ❌ error: cannot return a value from a void function

}

```
### 🔹 Key Takeaways
- Functions return **one value** to the caller via the `return` statement.
- Returned values can be ignored, used directly, or stored.
- `main()`’s return value is a **status code** for the operating system.
- Void functions have no return values
---
### 🧠 Flashcards
**Q1:** What are the **two things** needed for a function to return a value? 
**A1:**
- A **return type** → defines the type of value returned.
- A **return statement** → `return <expression>;` sends the value back.
---
**Q2:**  What happens during a **return by value**?  
**A2:**
- The return expression is evaluated.
- The result is **copied** back to the caller.
- The function immediately exits.
---
**Q3:**  How do you avoid calling the same function multiple times for the same value?  
**A3:**  Store the result in a variable and reuse it:
```cpp
int value { return7() };
```
---
**Q4:**  How many values can a function return directly?  
**A4:**  
Only **one value**.  
(Workarounds use structs, references, or tuples — covered later.)
___
**Q5:**  What does the value returned from `main()` represent?  
**A5:**  A **status code** to the operating system:
- `0` → Success (`EXIT_SUCCESS`)
- Nonzero → Error (`EXIT_FAILURE`)
___
**Q:** What does the `void` keyword in a function declaration indicate?  
**A:** That the function does **not return a value** to the caller.
___
**Q:** What happens if you try to use a `void` function inside an expression like `std::cout << printHi();`?  
**A:** It results in a **compiler error** because `void` functions don’t produce a value.
___
**Q:** Is a `return;` statement required in a `void` function?  
**A:** No — it's **optional** and only used to exit the function early.
___
**Q:** What happens if you try to `return` a value from a `void` function?  
**A:** It causes a **compiler error** — `void` functions can’t return values.
___
**Q:** Can `void` functions still produce side effects?  
**A:** Yes — they can **modify output**, **change reference variables**, or **perform actions** even though they return no value.

#flashcards 