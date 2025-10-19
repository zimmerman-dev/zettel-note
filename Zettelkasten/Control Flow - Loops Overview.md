♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:36 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #note #cpp [[Control Flow - For Loop]] , [[Control Flow - While Loops Examples]] , [[Control Flow - Do While Loop]] , [[Control Flow - Ranged For Loops]] , [[Control Flow - Nesting Loops]] 
___
## 📝 Note: Loops - Overview
While a **loop** might seem simple at first, it can introduce a surprising amount of complexity to a program’s control flow. To get started, let’s define **iteration**. Iteration refers to the repeated execution of a statement or block of statements. In C++, iteration is made possible through a control flow construct called a **loop**.

A loop is composed of two main parts:
- A **condition** that controls whether the loop continues running    
- A **body** that contains the code to repeat

The loop will continue to iterate _while_ or _until_ the condition evaluates to true (depending on the type of loop). That condition is checked at specific points in the loop’s lifecycle, and _when_ it’s checked has important consequences for how the loop behaves. We’re being intentionally general here because C++ provides **multiple kinds of loops**, each with its own rules and quirks. In the sections ahead, we’ll lock in more specific definitions for each one.
___
### 🔹 While Statements
The **`while` statement** (also called a **while loop**) is the simplest loop in C++. It behaves like an `if` statement, except that as long as the condition remains `true`, the loop body keeps executing.

Syntax:
```cpp
// ...
int x{0};

while (x <= 10) {
  std::cout << x << '\n';
}
```
> If it's just like an `if`, won't this run forever?

Yes. The `while` loop is what's called a **pre-test loop**, meaning the **condition is evaluated before** the body executes.  For the example above, the loop continues to execute as long as the condition remains true. Yet, if the condition happens to be initially false, the loop body will never run. 
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
#### Incrementation
To make a loop run a specific number of times, we modify `x` inside the loop:
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
___
### 🔹 Iterations
As previously stated, each time a loop executes, it's called an **iteration**. As we've seen, it's easy to repeat something every time through the loop. But what if you only want to do something on every 2nd, 3rd, or _nth_ iteration? This can be done by using the modulo operator:
```cpp
#include <iostream>

int main()
{
  int count{1};
  while (count <= 50) 
    {
    // print the number (first if statement is for formatting reasons)
    if (count < 10) 
    {
      std::cout << '0';
    }
    
    std::cout << count << ' ';
	// if the loop is divisible by 10, print a newline
    if (count % 10 == 0)
    {
      std::cout << '\n';
    }
    // increment the counter
    ++count;
  }
  return 0;
}
```
> Block scope added for clarity and formatting control

Output:
```text
01 02 03 04 05 06 07 08 09 10 
11 12 13 14 15 16 17 18 19 20 
21 22 23 24 25 26 27 28 29 30 
31 32 33 34 35 36 37 38 39 40 
41 42 43 44 45 46 47 48 49 50 
```
#### ⚠️ Common Practices and Pitfalls
1. Don’t accidentally put a semicolon after the while condition: `while (condition);`
   - This silently ends the loop body, and your actual loop block becomes unrelated.
1. Loop counters are often named `i`, `j`, `k`, etc. — a convention dating back to Fortran.
2. Avoid using unsigned loop variables. Signed integers are safer unless you **know** you're counting strictly in the positive.
___
### 🔹Loop Types
1. [[Control Flow - For Loop|For Loops]] - Controlled iteration with explicit index handling.
2. [[Control Flow - Ranged For Loops| Ranged based For loops]] - Simplified iteration over containers.
3. [[Control Flow - While Loops Examples| While Loops]] - Runs as long as a condition is true.
4. [[Control Flow - Do While Loop| Do while loops]] - Similar to while, but executes at least once.