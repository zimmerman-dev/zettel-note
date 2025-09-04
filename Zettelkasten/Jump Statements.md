 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚12:17 pm  📆 Mon Sep 1
 🔗 **Related Concepts**: #note #cpp [[Control Flow]]
___
## 📝 Note: Jump Statements
A jump statement is a control flow statement that unconditionally transfers the flow of the program execution to a different part of the code. Unlike conditional statements that rely on specific conditions to alter the flow, jump statements provide an immediate change in execution path.
### 🔹 `break`
**Use Case:** When you want to **stop a loop or switch** early.
```cpp
for (int i = 0; i < 5; ++i) {
    if (i == 3)
        break;  // If i is 3, exit the loop entirely
    std::cout << i << " ";
}
// Output: 0 1 2
```

>**Definition:**  
>If a specified condition is met, `break` **immediately exits the closest enclosing loop or switch statement**, skipping all remaining iterations or cases.
>---
### 🔹 `continue`
**Use Case:** When you want to **skip over specific cases** but keep looping.
```cpp
for (int i = 0; i < 5; ++i) {
    if (i == 2)
        continue; // If i is 2, skip printing and continue the loop
    std::cout << i << " ";
}
// Output: 0 1 3 4
``` 

> **Definition:**  
>If a specified condition is met, `continue` **skips the rest of the current loop iteration** and immediately jumps to the **next iteration** of the loop.
>---
### 🔹 `goto`
**Use Case:** Rarely used — mainly for **jumping out of deeply nested loops** or in legacy code
```cpp
int i = 0;
start:
if (i < 3) {
    std::cout << i++ << " ";
    goto start;
}
// Output: 0 1 2
```

>**Definition:**  
>Jumps to a _labeled_ statement elsewhere in the same function. **Generally discouraged** due to poor readability and error-prone behavior.
>---
### 🔹 `return`
**Use Case:** To **terminate a function early**, optionally with a result.
```cpp
int doubleOrZero(int x) {
    if (x == 0)
        return 0;  // Exit early if x is 0
    return x * 2;
}
// In main(), return 0; signals that the program ended successfully.
```

>**Definition:**  
>If a specified condition is met (or unconditionally), `return` **exits the current function immediately** and optionally sends back a value to the caller.
>---
### 🧠 Flashcards

**Q:** What does the `break` statement do in a loop or `switch`?  
?|?
**A:** It exits the nearest enclosing loop or `switch` immediately.

**Q:** What does `continue` do inside a loop?  
?|?
**A:** It skips the remaining loop body and moves to the next iteration.

**Q:** Why is `goto` discouraged in modern C++?  
?|?
**A:** Because it creates _spaghetti code_ and makes logic harder to follow and debug.

**Q:** What does a `return` statement do?  
?|?
**A:** It exits the current function and optionally returns a value to the caller.

#flashcards 