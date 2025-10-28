 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:46 am  📆 Thu Oct 16
 🔗 **Related Concepts**: #note #cpp [[Control Flow - Overview]] , [[Control Flow - Loops Overview]]
___
## 📝 Note: Control Flow - Break and Continue
In the case of the `switch` statement, we've already seen how `break` prevents fallthrough. But `break` isn’t limited to `switch`. When used in a `while`, `do-while`, or `for` loop, `break` **immediately exits the loop**, skipping all remaining iterations. Execution resumes with the first statement **after** the loop.

See: [[Control Flow - If Statement Alternatives (Switch)]] for how `break` behaves in `switch` statements.
### 🔹 Breaking a loop
In the context of a loop, a `break` statement can be used to end the loop early. For example:
```cpp
#include <iostream>

char getLet() {
  std::cout << "Enter a lowercase letter: ";
  char letter{};
  std::cin >> letter;
  return letter;
}

int main() {
  char myLetter{getLet()};
  char i{97};

  while (myLetter >= i) {
    if (myLetter > 122) {
      break;
    }
    std::cout << myLetter << " ";
    myLetter++;
  }
  return 0;
}
```
> This isn't the most efficient way to write this, but it clearly shows how `break` can exit a loop early. In this example, once the `break` is hit, control jumps past the `while` loop to the `return` statement, ending the program.
___
### 🔹 `break` vs `return`
New programmers tend to confuse `break` and `return`, but they are very much distinct from each other. As noted earlier, `break` exits only the control flow construct (like a loop), and execution resumes at the first statement **after** the loop or block. In contrast, `return` exits the entire function immediately, regardless of where it’s called, even from inside a loop. Control jumps back to where the function was called.
```cpp
#include <iostream>

char getLet() {
  std::cout << "Enter 'b' for break, 'r' for return: ";
  char ch{};
  std::cin >> ch;
  return ch;
}

int breakOrReturn() {
  while (true) {
    char ch{getLet()};
    if (ch == 'b') {
      break;
    }
    if (ch == 'r') {
      return 1;
    }
  }
  std::cout << "Break on free to the other side.\n";
  return 0;
}

int main() {
  int returnVal{breakOrReturn()};
  return 0;
}
```
### 🔹 `continue`
The **continue statement** provides a useful, convenient way to end the current iteration of a loop without exiting the loop entirely.

For example:
```cpp
#include <iostream>

int main() {
  for (size_t count{0}; count < 10; ++count) {

    if (count % 2 == 0) {
      continue;
    }
    std::cout << count << " ";
  }
  std::cout << '\n';
  return 0;
}
```
> You _could_ write this logic without `continue`, or even restructure it using `break`, but `continue` makes the intent **explicit**: skip this iteration, then keep going.
### 🔹 TL;DR
`break` – exits the loop immediately.  
  - No further statements in the loop body run.  
  - Control jumps to the first statement **after** the loop.

`continue` – skips the rest of the current iteration.  
  - Control jumps to the top of the loop and re-checks the condition.

`return` – exits the **entire function**, not just the loop.
___
### 🧠 Flashcards

What's the difference between `break` and `return` when used inside a loop?
?|?
`break` exits the loop but continues execution with the next statement **after** the loop.  
`return` exits the **entire function** immediately, regardless of whether it's inside a loop.

___

What happens if a `break` is triggered inside a `while` loop nested in a function?
?|?
The loop stops, but the function continues — execution resumes with the first line **after** the loop inside the function.

___

In this code, what is the output if the user enters `'r'`?

while (true) {
  char ch{getLet()};
  if (ch == 'b') break;
  if (ch == 'r') return 1;
}
std::cout << "Done\n";
?|?
The output is nothing — the `return` exits the entire function **before** `std::cout` is reached.

___

What is the effect of a `continue` statement inside a `for` loop?
?|?
It skips the **rest of the current iteration**, jumps to the **increment step**, then re-checks the loop condition.

___

When should you use `continue` instead of restructuring logic with `if` or `break`?
?|?
Use `continue` when you want to *explicitly skip just one iteration* of a loop, without ending the loop or deeply nesting logic. It improves clarity when that’s your precise intent.


#flashcards 