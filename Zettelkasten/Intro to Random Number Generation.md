 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚6:40 pm  📆 Tue Oct 28
 🔗 **Related Concepts**: #note #cpp
___
## 📝 Note: Intro to Random Number Generation
At first glance, generating random numbers seems like a simple task, and in some ways, it is. It’s easy to **simulate** randomness, or to create something that _looks_ unpredictable. But in truth, producing real randomness, especially in software, is much harder than it seems.

In the real world, we often rely on physical events like flipping a coin or rolling dice. These actions _feel_ random because they’re incredibly difficult to predict, which makes it random _enough_ for most purposes, like deciding who starts in a baseball game, or who gets to sit shotgun on the ride home.

Computers, however, are deterministic machines. They can’t generate true randomness on their own. What they _can_ do is simulate randomness using carefully designed algorithms. These are called **pseudorandom number generators (PRNGs)**, and while they **don’t produce true randomness**, they’re often good enough to fool both humans and machines.
___
### 🔹 Algorithms and State
An **algorithm** is a finite sequence of instructions that can be followed to solve some problems or produce some useful result. For example, lets say you have a formula to find the area of a rectangle and you wanted to create and algorithm from that formula.

```cpp
#include <iostream>

int areaRectangle(int length, int width) {
  return length * width;
}

int main() {
  // ...
  std::cout << "Area: " << areaRectangle(length, width) << '\n';
  return 0;
}
```
> This simple algorithm helps demonstrate the difference between what a *formula* and an *algorithm* is.

A **formula** is what expresses what the result is in mathematical terms, and it's what makes up the DNA of the algorithm. In this case, it's just: 
- ($area = length * width$).

An **algorithm** the *set of steps* that carries out the formula in a usable way, like in code. Since the example is relatively simple, the algorithm is:
- `return length * width;`
___
### 🔹 State
When working with algorithms, it’s important to understand what the term **state** means.

> An **algorithm is stateful** if it **remembers information between calls**. An **algorithm is stateless** if it **doesn’t retain any memory**, and must be given **everything it needs** every time it runs.

The two examples below produce similar outputs — but solve the problem in **very different ways**:
--- start-multi-column: ID_7im6
```column-settings
Number of Columns: 2
Largest Column: Standard
Column Spacing: 3px
Border: off
Overflow: Hidden
```
```cpp
#include <iostream>

int plusOne() {
  static int s_state{1};

  s_state++;
  return s_state;
}

int main() {
  std::cout << plusOne() << '\n';
  std::cout << plusOne() << '\n';
  std::cout << plusOne() << '\n';
  return 0;
}
```
> 📌 In this version, the algorithm **manages its own memory** using `static`, and remembers its state across calls. 

--- column-break ---
```cpp
#include <iostream>

int plusOne(int i) {
  i++;
  return i;
}

int main() {
  int state{1};
  std::cout << plusOne(state) << '\n';
  state++;
  std::cout << plusOne(state) << '\n';
  state++;
  std::cout << plusOne(state) << '\n';
  return 0;
}

```
> 📌 In this version, the algorithm is **stateless** — the caller must keep track of the changing state and pass it in every time.

--- end-multi-column
The **stateful** version wraps the logic neatly into a self-contained function. It manages its own internal memory (`s_state`) using a `static` variable, allowing it to track progress over time without the caller needing to maintain state.

This version is **deterministic** in the sense that, if it starts from the same internal state (`s_state = 1`), it will always produce the **same output sequence** every time the program is run. Its behavior depends on past executions, but is still fully predictable if the starting conditions are known.

> This is exactly how many random number generators work — they aren't truly random, but **deterministic algorithms** that evolve state to produce values that _look_ unpredictable.
___

### 📌 Key Definitions

___
### 🧠 Flashcards
