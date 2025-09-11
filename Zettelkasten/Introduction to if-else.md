 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚11:12 pm  📆 Tue Sep 9
 🔗 **Related Concepts**: #note #cpp [[Boolean Logic]] , [[Control Flow]] , [[Literals & Operators]], [[Statements and Expressions]] , [[Boolean Type]]
___
## 📝 Note: If Statements
The `if` statement is a simple but powerful tool that introduces **conditional flow** into your programs. The idea is straightforward:

> "**If** a condition is `true`, execute the associated statement."

This allows your code to respond dynamically — skipping or executing logic depending on what's happening during runtime. Along with `else if` and `else`, the `if` statement forms the backbone of decision-making in C++.
### 🔹 Syntax:
```cpp
if (condition) {
// true_statement
}
```

If the *condition* of an `if` statement evaluates to Boolean value `true`, then the *true_statement* is executed. If the *condition* instead evaluates to Boolean value `false`, then *true_statement* is skipped.
#### Sample 1
```cpp
#include <iostream>

int main() {
  std::cout << "Enter an Integer: ";
  int x{};
  std::cin >> x;

  if (x == 0) {
    std::cout << "Your entered zero. \n"; 
  }
  return 0;
}
```
> The sample program is simple, and it obviously doesn't check for every scenario, but it should paint a picture at how useful it can be. With one conditional flow tool, we can chain together many of these `if` clauses to follow generally simple, yet deep instructions.

Given what we know about the last example, how would you go about adding extra complexity to check for edge cases? You *could* stack another `if` clause, like this:
#### Sample 2
```cpp
#include <iostream>

int main() {
  std::cout << "Enter an integer: ";
  int x{};
  std::cin >> x;

  if (x == 0) {
    std::cout << "Your value is zero";
  }
  if (x != 0) {
    std::cout << "Your value is non-zero";
  }
  return 0;
}
```
> This works, and we *could* theoretically just keep adding `if` clauses over, and over again. However, there are more elegant ways to solve this issue.
### 🔹 `if` and `else`
After you're comfortable with the `if` clause, we can look at adding it's logical counterpart, the `else` clause. If the `if` clause is like saying, "If a condition is true, execute the associated statement...", the `else` is like saying "*Otherwise*" at the end of that statement.
### 🔹 Syntax
```cpp
if (condition) {
	// true_statement
} else {
	// false_statement
}
```
> *If condition is true, execute true_statement. Otherwise, execute false_statement.*

Lets amend Sample 2 with our new `if-else` conditional block.
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
> Now, for all intents and purposes, these two program do behave *similarly*, but they are different. We will get into that more later, but simply, we can see how in Sample 2, the second `if` clause checks if x != 0, while in our amended program, else just acts like a sort of catch-all for any value thats not zero.
### 🔹 `if`, `else if`, and `else`
If we want to be ultra precise and catch even more edge cases, we can combine Sample 1, Sample 2, and our amended Sample 2 program. By that I mean we can chain `if` clauses together, and use the `else` clause.

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
> With this, our logic tree is starting to take real shape. It's not checking for every edge case, but this note, it shows how much complexity can be had with very little effort.
















___
### 📌 Key Definitions
- **Condition**: Or *conditional expression* is an expression that evaluates to a Boolean value. 









___
### 🧠 Flashcards

