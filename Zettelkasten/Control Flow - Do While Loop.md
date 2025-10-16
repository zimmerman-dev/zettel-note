♻️ (*MinGW, Windows11, Codelite*)   
 ⌚11:24 pm  📆 Sat Aug 2
 🔗 **Related Concepts**: #cpp #note  [[Control Flow - Loops Overview]]
___
## 📝 Note: Loops - Do While Loop
The `do-while` statement dates back to the 1960s, originating in **ALGOL-60** and **ALGOL-68**. In the 1970s, Dennis Ritchie introduced it into the C programming language during a time when **structured control flow** was becoming a key principle in modern programming.

Much like the `while` statement, the `do-while` loop does what it sounds like: it executes a block of code once, then checks a condition to decide whether to repeat. Unlike `while`, the condition is evaluated **after** the block runs — guaranteeing that the loop body executes **at least once**.

The loop continues as long as the condition remains `true`, or until an early exit via `break`.
___
### 🔹 `do-while` Syntax
```cpp
do {
	statements;
} while (expression);
```    
#### Example:
```cpp
// ...
  int selection{};
  do {
    std::cout << "Menu (1)\n";
    std::cout << "Menu (2)\n";
    std::cout << "Menu (3)\n";
    std::cout << "Pick 1-3: ";
    std::cin >> selection;
  } while (selection < 1 || selection > 3);
  
  // switch (selection) ...
```
> This example showcases a simple menu system if followed up with something like a switch statement. There are other ways you could do this, but this example showcases the structured control flow that was used to replace `goto`-like constructs.
___
### 🔹 When to Use
Use a `do-while` loop when you want a block of code to execute **at least once**, and then **repeat only while** a certain condition remains true.

- ✅ When the **first iteration must always run**, regardless of the condition
- ✅ Menu systems where the menu should display at least once
- ✅ Input prompts where the user should be asked at least once before validation
- ✅ Retry mechanisms where the action should attempt first, then check for continuation
### 🔹 Key Difference from `while`
While the `while` loop is a pre-test loop, a `do while` loop is a post-test loop meaning that the **condition is evaluated after** the loop body runs once. Therefore, the loop body **always executes at least once**, even if the condition is false initially.
___
### 🧠 Flashcards

What structural advantage does a `do-while` loop have over a `while` loop when designing user input validation systems?  
?|?  
It guarantees that the prompt and input logic execute at least once before any condition is checked, allowing cleaner validation loops without duplicated code or pre-loop flags.

---

You see a loop that always executes once and then terminates, even though its condition is `false`. Is this undefined behavior in C++? Why or why not?  
?|?  
No — this is expected behavior for a `do-while` loop. Since the condition is checked _after_ the first iteration, the loop will always run once, even if the condition is false from the start.

---

Which of the following loop types best expresses "try something once, then keep retrying _only if needed_"?  
A) `while`  
B) `for`  
C) `do-while`  
D) `goto`  
?|?  
C) `do-while` — it's the only standard loop form that ensures the first attempt happens before any condition is evaluated.

---

How does putting the loop condition at the bottom (in a `do-while`) affect how readers understand control flow compared to `while` or `for`?  
?|?  
It delays understanding the exit condition, making it harder to immediately grasp the loop's control logic. Readers must scroll or read the whole body to understand the loop's termination criteria.

---

You refactor a `do-while` loop into a `while (true)` with a `break`. What benefit might this give you in certain cases?  
?|?  
It allows for multiple `break` points and clearer exit conditions inside the loop body, which can improve readability when loop termination logic is complex or depends on multiple factors.

#flashcards 