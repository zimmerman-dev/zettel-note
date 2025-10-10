 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:54 pm  📆 Sat Sep 13
 🔗 **Related Concepts**: #note #cpp [[Control Flow - Overview]] , [[Control Flow - Conditional Statements Overview]] , [[Statements and Expressions]] , [[Operators - Overview]] , [[Boolean Logic]] , [[Functions - Return]]
___
## 📝 Note: Control Flow - If Statement Basics
The `if` statement introduces **conditional flow** into a program—one of the most fundamental ways to make your code react to what's happening at runtime.

> “**If** a condition is `true`, execute the associated statement.”

That’s it. Just one fork in the road, and suddenly your code can branch, adapt, and decide. This forms the backbone of most logic in C++, along with `else if` and `else`.
___
### 🔹 Syntax
```cpp
if (condition) {
  // statement(s)
}
```
If the `condition` evaluates to the Boolean value `true`, then `true_statement` runs. If it evaluates to `false`, the statement is skipped entirely.
___
### 🔹 Sample 1: Basic Check
```cpp
#include <iostream>

int main() {
  std::cout << "Enter an integer: ";
  int x{};
  std::cin >> x;

  if (x == 0) {
    std::cout << "You entered zero.\n";
  }
  return 0;
}
```
 This basic check illustrates the core idea: _only_ if the condition is met, the block executes. Otherwise, the program skips it entirely and keeps going.
 
___
### 🔹 Sample 2: Stacking `if` statements
Now suppose we want to handle both zero and non-zero input:
```cpp
#include <iostream>

int main() {
  std::cout << "Enter an integer: ";
  int x{};
  std::cin >> x;

  if (x == 0) {
    std::cout << "Your value is zero\n";
  }
  if (x != 0) {
    std::cout << "Your value is non-zero\n";
  }
  return 0;
}
```
This technically works. But it’s clunkier than it needs to be—each condition is checked independently, even when they’re logically exclusive. A more elegant option? Let’s add a **fallback**.
___
### 🔹 `if` and `else`
The `else` clause is the natural companion to `if`. If `if` says, _“do this if true”_, then `else` says, _“otherwise, do this instead.”_
#### Syntax:
```cpp
if (condition) {
  // true_statement
} else {
  // false_statement
}
```

Here’s that same program, rewritten with `else`:
```cpp
#include <iostream>

int main() {
  std::cout << "Enter an integer: ";
  int x{};
  std::cin >> x;

  if (x == 0) {
    std::cout << "Your value is zero.\n";
  } else {
    std::cout << "Your value is non-zero.\n";
  }
  return 0;
}
```
Now only **one** branch executes. This isn’t just cleaner—it’s more efficient.
___
### 🔹 `if`, `else if`, and `else`
To handle multiple distinct paths, we can chain conditions together using `else if`. Each one is only checked if all previous conditions failed.

```cpp
#include <iostream>

int main() {
  std::cout << "Enter an integer: ";
  int x{};
  std::cin >> x;

  if (x > 0) {
    std::cout << "Your value is positive\n";
  } else if (x < 0) {
    std::cout << "Your value is negative\n";
  } else {
    std::cout << "Your value is zero.\n";
  }
  return 0;
}
```
This pattern gives us a structured logic tree. Only one branch will ever execute—whichever condition passes first. See [[Operators - Overview]] and [[Statements and Expressions]].
___
### 🔹 Using Functions that Return `bool`
You can pass conditions into `if` statements from **any expression that returns a Boolean**, including your own functions.

```cpp
bool isEqual(int x, int y) {
  return x == y;
}
```

We can plug this directly into an `if`:
```cpp
#include <iostream>

bool isEqual(int x, int y) {
  return x == y;
}

int main() {
  std::cout << "Enter an integer: ";
  int x{};
  std::cin >> x;

  std::cout << "Enter another integer: ";
  int y{};
  std::cin >> y;

  std::cout << std::boolalpha;

  if (isEqual(x, y)) {
    std::cout << x << " and " << y << " are equal!\n";
  } else {
    std::cout << x << " and " << y << " are not equal!\n";
  }

  return 0;
}
```

This is a powerful combo. Clean comparisons, reusable logic, and concise flow.
___
### 🔹 Best Practices
-   Use `else` and `else if` when conditions are **mutually exclusive**.    
-   Prefer braces `{}` even for single-line blocks. It’s safer and easier to refactor later.    
-   Keep conditions **simple and expressive**: `isReady()`, `x < 10`, `buffer.empty()`.    
-   Return early when it makes the logic easier to follow—don’t nest unnecessarily.
___
### 📌 Key Definitions
-   **Condition**: An expression that evaluates to a Boolean (`true` or `false`). Can be a comparison, a function call, or any Boolean-producing expression.
-   **Early Return**: Using `return` to exit a function as soon as a condition is met—often used to simplify logic and avoid deep nesting.
___
### 🧠 Flashcards

**Q:** What happens if an `if` condition evaluates to false?  
?|?
**A:** The associated statement block is skipped.

___

**Q:** Why use `else` instead of a second `if`?  
?|?
**A:** `else` prevents unnecessary checks and guarantees only one path runs.

___

**Q:** What is the purpose of `else if`?  
?|?
**A:** To check a new condition _only_ if all previous ones failed.

___

**Q:** Can a function returning `bool` be used in `if`?  
?|?
**A:** Yes—its result is evaluated as the condition.

___

**Q:** What’s an early return and when is it useful?  
?|?
**A:** It exits a function before the end. Use it to avoid unnecessary work or nested logic.

#flashcards 