 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:46 am  📆 Thu Oct 16
 🔗 **Related Concepts**: #note #cpp
___
## 📝 Note: Control Flow - Break and Continue
In the case of the `switch` statement (_😉pun intended_), we've already seen how `break` can be used to prevent fallthrough. However, `break` isn’t limited to `switch`, it can also be used in all manners of control flow statements. When used in a `while`, `do-while`, or `for` loop, the `break` statement **immediately exits the loop**, skipping any remaining iterations. Execution continues with the first statement **after** the loop.

See: [[Control Flow - If Statement Alternatives (Switch)]] to see how `break` works for `switch` statements.
### 🔹 Breaking a loop
In the context of a loop, a `break` statement can be used to end the loop early. For example:
```cpp
#include <iostream>

int main() {

}
```
`break` – exits the loop immediately.  
  - No further statements in the loop body run.  
  - Control jumps to the first statement **after** the loop.

`continue` – skips the rest of the current iteration.  
  - Control jumps to the top of the loop and re-checks the condition.

`return` – exits the **entire function**, not just the loop.

___
### 📌 Key Definitions

___
### 🧠 Flashcards
