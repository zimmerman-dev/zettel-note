♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:36 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #note #cpp [[Control Flow - For Loop]] , [[Control Flow - While Loops]] , [[Control Flow - Do While Loop]] , [[Control Flow - Ranged For Loops]] , [[Control Flow - Nesting Loops]] 
___
## 📝 Note: Loops - Overview
While a **loop** might seem simple at first, it can introduce a surprising amount of complexity to a program’s control flow. To get started, let’s define **iteration**. Iteration refers to the repeated execution of a statement or block of statements. In C++, iteration is made possible through a control flow construct called a **loop**.

A loop is composed of two main parts:
- A **condition** that controls whether the loop continues running    
- A **body** that contains the code to repeat

The loop will continue to iterate _while_ or _until_ the condition evaluates to true (depending on the type of loop). That condition is checked at specific points in the loop’s lifecycle, and _when_ it’s checked has important consequences for how the loop behaves. We’re being intentionally general here because C++ provides **multiple kinds of loops**, each with its own rules and quirks. In the sections ahead, we’ll lock in more specific definitions for each one.
___
### 🔹 While Statements
The **`while` statement** (also called a **while loop**) is the simplest loop in C++. It behaves like an `if` statement — except that as long as the condition remains `true`, the loop body keeps executing.

Syntax:
```cpp
// ...
int x{0};

while (x <= 10) {
  std::cout << x << '\n';
}
```
> If it's just like an `if`, won't this run forever?

Yes. That’s an **infinite loop**. The condition `x <= 10` is always true unless `x` changes, and since nothing modifies `x`, the loop never ends.

To make it run a specific number of times, we modify `x` inside the loop:
```cpp
#include <iostream>

int main() {
  int x{0};

  while (x <= 10) {
    std::cout << x << '\n';
    ++x;
  }

  return 0;
}
```
> Now `x` increases by 1 each time the loop runs. Once `x` is 11, the condition fails and the loop ends.
#### Intentional Infinite Loops
Sometimes you _do_ want an infinite loop (e.g., in games or embedded systems). In those cases, make your intent obvious. Don’t rely on a condition that _looks_ like a mistake.

Preferred form:
```cpp
// ...

while (true) {
  // Do something forever;
}
```
> This makes it clear that the loop is meant to run endlessly, not just missing a condition or increment.
___
### 🔹 Common Practices and Pitfalls
1. Do not accidentally put a semicolon after the while condition, i.e., `while (condition);`. This is a fairly common footgun to watch for.
2. Loop variables are commonly simply named, `i`, `j`, `k`, etc. This is a convention that has persisted since the Fortran days.
3. Variable loops should almost always be signed, as unsigned integers can lead to unexpected problems.


### 🔹 **Control Statements**
- `break` – exits the loop early.
	- No further statements in the body of the loop are executed
	- Loop is immediately terminated
	- Control immediately goes to the statement following the loop construct

- `continue` – skips the rest of the current iteration and moves to the next.
	- No further statements in the body of the loop are executed
	- Control immediately goes directly to the beginning of the loop for the next iteration

- `return` – exits the entire function, not just the loop.

---
### 🔹 **Loop Types**
#### [[Control Flow - For Loop|For Loops]] 
- Controlled iteration with explicit index handling.
#### [[Control Flow - Ranged For Loops| Ranged based For loops]] 
- Simplified iteration over containers.
#### [[Control Flow - While Loops| While Loops]] 
- Runs as long as a condition is true.
#### [[Control Flow - Do While Loop| Do while loops]]
- Similar to while, but executes at least once.
___
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