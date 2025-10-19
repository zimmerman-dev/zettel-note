♻️ (*MinGW, Windows11, Codelite*)   
 ⌚4:12 pm  📆 Sat Aug 2
 🔗 **Related Concepts**: #cpp #note [[Control Flow - Loops Overview]], [[Operators - Increment & Decrement]]
___
## 📝 Note: Control Flow - For Loop
One of the most commonly used loop types in C++ (and many other higher-level languages) is the classic `for` loop. The `for` loop is ideal when there’s a clear loop variable, because it allows us to **declare**, **test**, and **update** it all in one place.

As of C++11, there are two kinds of `for` loops, but this note will focus specifically on the **classic** form.
___
### 🔹 `for` Syntax
```cpp
for (initializer; condition; iterator expression) {
  // Statement ...
}
```

Example:
```cpp
for (int i{1}; i < 10; ++i) {
  // statement (executes while i is less than 10)
}
```
> Notice the while word in the comment? Interesting! 

An easy way to understand the `for` loop is by making a subtle translation into a `while` loop:
```cpp
int i{1};           // initializer
while (i < 10) {    // condition
  // statement
  ++i;              // iterator expression
}
```
___
### 🔹 Evaluation of `for`
A `for` loop is evaluated in three parts:
1. The **initializer** executes once at the start of the loop. If it declares a variable, that variable has **loop-local scope**.  
2. With each iteration, the **condition** is evaluated. If `true`, the loop body executes. If `false`, the loop terminates and execution continues with the statement after the loop.    
3. After the loop body runs, the **end-expression** (usually an iterator or increment statement) is executed.
#### Key insight
There are two big things to remember:
- First, the loop body **executes before** the end-expression. This can feel a bit unintuitive; the update expression runs **after** the body, but **before** the condition is rechecked on the next pass.
- Second, remember that **loop-local scope** means the initializer variable dies when the loop ends. If the loop is entered multiple times (e.g. in a nested loop scenario), the initializer is re-executed, and the variable is reset to its original starting value.  This will become important later when we cover **nested `for` loops**. You’ll want to come back and revisit this.
___
### 🔹 `operator!=` (Warning)
Let’s compare two different loops that seem identical on the surface:
```cpp
// loop 1
for (auto i{0}; i < 10; ++i) {
  std::cout << i << '\n';
}

// loop 2
for (auto x{0}; x != 10; ++x) {
  std::cout << x << '\n';
}
```
> Which block of code do we prefer? Why?

At first glance, `!= 10` may seem harmless. But the difference becomes more apparent with even a small change:
```cpp
  for (auto i{1}; i < 10; ++i) {
    std::cout << i << '\n';
    if (i == 9)
      ++i;
  }
  
  // vs 
  
  for (auto x{1}; x != 10; ++x) {
    std::cout << x << '\n';
    if (x == 9)
      ++x;
  }
```
#### Behavior Comparison
- In the **first loop**, the condition `i < 10` ensures the loop ends cleanly when `i` becomes 10. Even if we manually increment `i` inside the loop, we _can't skip past_ the stop condition — it will still terminate cleanly.
    
- In the **second loop**, we use `x != 10` as the stopping condition. If we manually increment `x` past 10 (e.g. to 11), the condition remains true — `11 != 10`. This results in the loop **continuing past the intended stop**, potentially forever.


> ✅ Prefer `< limit` over `!= limit` in counting loops — it’s safer, less error-prone, and protects against accidentally skipping the sentinel value.
___
### 🧠 Flashcards

**What are the three components of a classic `for` loop?**  
?|?  
Initializer, condition, iterator expression

---

**When is the initializer of a `for` loop executed?**  
?|?  
Once, at the beginning of the loop

---

**What happens after the loop body executes in a `for` loop?**  
?|?  
The iterator expression runs, then the condition is rechecked

---

**What does it mean when a loop variable has "loop-local scope"?**  
?|?  
It means the variable exists only within the loop and is destroyed when the loop ends

---

**Convert this `for` loop into an equivalent `while` loop: `for (int i = 0; i < 5; ++i)`**  
?|?
```cpp
int i = 0;  
while (i < 5) {  
  // body  
  ++i;  
}
```

___

**Why is `i < 10` preferred over `i != 10` in counting `for` loops?**  
?|?  
Because skipping over 10 causes `< 10` to stop safely, while `!= 10` keeps running, potentially forever.

___

**What happens if a loop variable using `!=` skips over the sentinel value?**  
?|?  
The loop becomes infinite, because the stop condition (`x != sentinel`) is never met

---

**When does the iterator expression run in a `for` loop? Before or after the condition?**  
?|?  
After the body, but before the next condition check.