♻️ (*MinGW, Windows11, Codelite*)   
 ⌚4:12 pm  📆 Sat Aug 2
 🔗 **Related Concepts**: #cpp #note [[Control Flow - Loops Overview]], [[Operators - Increment & Decrement]]
___
## 📝 Note: Control Flow - For Loop
One of the most commonly used loop types in C++ (and many other higher-level languages) is the classic `for` loop. The `for` loop is ideal when there’s a clear loop variable, because it allows us to **declare**, **test**, and **update** it all in one place. As of C++11, there are two kinds of `for` loops, but this note will be specifically dedicated to the classic `for` loop.
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
  // statement <--> (executes while i is less than 10)
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

### 📌 Key Definitions

___
### 🧠 Flashcards





A traditional `for` loop is ideal when you need to iterate a **specific number of times** or require control over the loop variable.

```cpp
for (initialization; condition; increment) {
    statement;
}
```    
### 🔹**How It Works**
1. **Initialization** – executes once, setting up the loop control variable.  
2. **Condition** – checked **before each iteration**.  
   - If `true`, the loop body executes.  
   - If `false`, the loop terminates.  
3. **Body** – the statements inside the braces run when the condition is true.  
4. **Increment/Decrement** – updates the loop variable, then returns to the condition check.
### 🔹 **Example**
```cpp
for (int i = 0; i < 5; i++) {
    std::cout << i << " ";
}
```
>Output:  `0 1 2 3 4`

- `i` starts at 0 (**initialization**)  
- The condition `i < 5` determines whether the loop continues  
- After each iteration, `i++` runs, and the cycle repeats until the condition is false  
###  🔹 **When to Use**
- ✅ Counting iterations  
- ✅ Iterating over a specific range or subset  
- ✅ When loop control (init, condition, update) should be explicit at the top  