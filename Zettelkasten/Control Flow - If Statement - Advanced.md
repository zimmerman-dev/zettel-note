 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚8:47 pm  📆 Wed Oct 8
 🔗 **Related Concepts**: #note #cpp [[Control Flow - If Statement - Basics]] , [[Control Flow - Conditional Statements Overview]]
___
## 📝 Note: Control Flow - If Statement - Advanced
In our introductory note [[Control Flow - If Statement - Basics]], we learned a lot of the basics about the `if` and `if-else` statements. First we'll recap, but consider the first note *Control Flow - If Statement Basics* as required prerequisite reading.
### 🔹 `if` Recap
The most basic kind of conditional statement in C++ is the `if statement`.
```cpp
if (condition)
  // statement executes when condition is true
```
> The `if` keyword executes a statement or block **only if the condition is true**.  If the condition is false, the block is skipped and the program continues.

Or with an optional `else statement`
```cpp
if (condition)
  // ...
else
  // statement executes if the condition is false
```
> When an `else statement` is present, its statement will execute if the condition for the `if statement` is false.
___
### 🔹 Implicit Blocks
When you write an `if statement` like this:
```cpp
if (condition)
  std::cout << "The condition is true!";
```

The compiler behaves like the statement is written like this:
```cpp
if (condition) {
  std::cout << "The condition is true!";
}
```
This is called an **implicit block**. when the programmer doesn't explicitly declare a block, the compiler treats the next statement as if it's inside one.

The rule about blocks is this:
**If your `if statement` or `else statement` only contains a single statement, you don't need braces.**

This:
```cpp
if (condition)
  std::cout << "Hello ";
  std::cout << "World." << '\n';
```

is actually seen by the compiler as this:
```cpp
if (condition) {
  std::cout << "Hello ";
} 
std::cout << "World. " << '\n';
```

The debate to block single line statements for `if` or `else` statements is ongoing. Everyone seems to have an opinion on whether you should or not. My two cents takes two things into account. Firstly, whether you believe you should or not doesn't really matter if the place you work at, or your school enforces a style guide. Secondly, if you don't have to conform to a style guide, consider what is the best way to be explicit and clear with your code. For me, that means using blocks every time. It's consistent, readable, and expressive.
___
### 🔹  `else if` Statements
```cpp
if (condition_1) {
    statement_1;
} else if (condition_2) {
    statement_2;
} else {
    statement_3;
}
```
> The `else if` construct chains multiple conditions together.  
> If the first condition is false, the program checks the next `else if`, and finally executes the `else` block if none match.

#### `if-else` vs `if-if`
When you first start out, you may wonder when it's most appropriate to use `if-else` instead of back-to-back `if` statements.
- Use `if-else` when you only want to execute the code after the first `true` condition.
- Use `if-if` when you want to execute the code after all `true` conditions.
___
As you probably know, if we want to add complexity to our conditional statements, we can nest our `if-else` statements. However consider a program like this:
### 🔹  Nested `if-else` Statements
It is possible to nest `if-else` statements: 

```cpp
if (condition_1) {
    if (condition_1a) {
        statement_1;
    } else {
        statement_2;
    }
} else {
    statement_3;
}
```
> Nesting allows multiple levels of conditions.  However, **deep nesting** can hurt readability; `else if` is often cleaner.
___
### 🔹 The Dangling `else` Problem
Consider the following program:
```cpp
#include <iostream>

int main() {
  
  std::cout << "Enter a num: ";
  int num{};
  std::cin >> num;

  if (num >= 0)
    if (num <= 20)
      std::cout << num << " is between 0 and 20." << '\n';
  else 
    std::cout << num << " is negative." << '\n';
    
  return 0;
}
```
> This is what is known as **the dangling else problem**, and it's when your `if-else` statements introduce ambiguity of ownership for the `else` statement at the end. What happens in this scenario is the compiler matches the `else` statement with the last unpaired `if` statement. This kind of bug is dangerous because the code compiles and runs — but not how you intended. These logic errors can be subtle and hard to catch.

What the compiler actually sees is something like this:
```cpp
#include <iostream>
// ...
      if (num <= 20) 
          std::cout << num << " is between 0 and 20." << '\n';
      else
          std::cout << num << " is negative." << '\n';
  }
// ...
```
> Like we talked about, we should be using braces to explicitly declare the scope of our statements. In the example above, the logical branching is mixed up because num being negative logically follows if the first `if` statement condition is false.  

 If we wanted to fix this, it would look like this:
```cpp
#include <iostream>

int main() {
    std::cout << "Enter a num: ";
    int num{};
    std::cin >> num;
    
    if (num >= 0) 
    {
        if (num <= 20) 
        {
            std::cout << num << " is between 0 and 20.\n";
        } 
        else if (num > 20) 
        {
            std::cout << num << " is greater than 20.\n";
        }
    } 
    else 
    {
        std::cout << num << " is negative.\n";
    }
    return 0;
}
```
> For the record, I usually use a more compact way of styling blocks, but this way is very clear on the nesting. 
 
If you want to **flatten** this, you can use some logical operators, especially in scenarios where the logic is so simple, like this one.
```cpp
// ...
if (num >= 0 && num <= 20) {
  std::cout << num << " is between 0 and 20" << '\n';
  // ...
```
___
### 🔹 Null Statements
A **null statement** is an expression that consists of just a semicolon.
```cpp
if (condition) {
  ; // Null statement
}
```
> To be precise, a null statement quite simply does nothing. We'll see later in loops where they are more effective. 

Just be careful not to do something like this:
```cpp
if (condition); // Not ok
```
This ends the `if` immediately. The body is empty, and any indented lines that follow are **not** part of the conditional, even though they _look like they are_.
___
### 🔹 `constexpr` with `if` Statements
Normally, the conditional of an `if` statement is evaluated at runtime; **however**, consider when the conditional is a constant expression, such as in the following example:
```cpp
// ...
int main() {
  constexpr double gravity{9.8};
  
  if (gravity == 9.8) {
    std::cout << "Gravity is normal.\n";
  } else {
    std::cout << "We are not on Earth!\n";
  }
  return 0;
}
```
> Because `gravity` is `constexpr` and initialized to `9.8`, the conditional `gravity == 9.8` must evaluate `true`. As a result, the `else` statement will never execute. (Evaluating a `constexpr` at runtime is wasteful. It's also wasteful to compile code into the executable that can never be executed).
___
### 🔹 `constexpr if` Statements (C++17)
The C++17 standard introduced the **constexpr if-statement**, which requires the conditional to be a constant expression. The conditional of a `constexpr if` statement will be evaluated at compile time. In simple terms, The purpose of `if constexpr` is to simplify decision-making during compilation by removing unnecessary or invalid code paths. If the condition is `true`, the compiler keeps the `if` block and discards the `else`.  If `false`, it does the opposite, long before the program runs. The compiler then is able to discard what isn't used.

In other words, this:
```cpp
#include <iostream>

int main() {
  constexpr double gravity{ 9.8 };

  if constexpr (gravity == 9.8) // now using constexpr if
	std::cout << "Gravity is normal.\n";
  else
	std::cout << "We are not on Earth.\n";
	
  return 0;
}
```

Compiles like this:
```cpp
// ...
int main() {
  constexpr double gravity{9.8};

  std::cout << "Gravity is normal.\n";

  return 0;
}
```
___
### 🧠 Flashcards
