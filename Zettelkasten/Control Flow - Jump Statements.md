 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚12:17 pm  📆 Mon Sep 1
 🔗 **Related Concepts**: #note #cpp [[Control Flow - Overview]]
___
## 📝 Note: Jump Statements
Broadly, the *conditional* statement is a construct that allows a program to execute different blocks of code based on whether a specified **condition** evaluates `true` or `false` (like the `if-else` statements from past notes). In contrast, an _unconditional_ statement; or more specifically for this note, a **jump statement** alters the flow of a program by forcing an immediate _jump_ to a different location in the code, regardless of any condition.

In [[Control Flow - If Statement Alternatives (Switch)]], we covered both `break` and `return`, which are actually examples of **jump statements**. These keywords interrupt the normal top-to-bottom execution order:
- `break` exits a `switch` or loop early.
- `return` exits a function, optionally returning a value.

You’ll encounter `break` again in [[Control Flow - Loops Overview]] and its child notes, where it’s commonly used to exit loops early. For `return`, the most in-depth treatment appears in the function-related notes, especially [[Functions - Return]]. Now that we’ve seen jump statements that serve clear and structured purposes, we’re ready to look at a **less structured** one: `goto`.
___
### 🔹 `goto` Statements
The `goto` statement is an unconditional jump statement that uses the `goto` keyword and a **statement label** to determine where the execution should jump.
```cpp
#include <iostream>
#include <cmath>

int main() {

tryAgain:  // Statement label
  std::cout << "Enter a non-negative number: ";
  int num{};
  std::cin >> num;

  if (num < 0) {
    goto tryAgain;  // goto statement
  }

  std::cout << "The square root of " << num << " is " << std::sqrt(num) << '\n';
  return 0;
}
```
> This program behaves similarly to a `while` loop, but mechanically it's not really a loop at all. The user is asked to enter a non-negative number. If a negative number is entered, the program uses `goto` to jump back to the labeled line `tryAgain`.

Unlike a loop, which is **conditional** by nature, repeating _while_ a condition is true, a `goto` is an **external control mechanism**. It does not form a logical circular structure; it simply jumps unconditionally when called, regardless of the larger control flow.
___
### 🔹 Statement Labels - Function Scope
We covered **local and global scope** in [[Namespaces, Scope, and Linkage]]. However, **statement labels** utilize a third type called **function scope**. This means that the `statement label` is visible throughout the function, even before the label itself is declared. 

For example:
```cpp
#include <iostream>

void printJump(bool jump) {
  if (jump)
    goto end;

  // ⬇️ Prints when jump == false; return prevents fallthrough to label
  std::cout << " jump over the brown dog!\n";
  return;

end:
  // Only prints when jump == true
  std::cout << "Cats";
}

int main() {
  printJump(true);
  printJump(false);
}
```

 ⚠️ Statement labels must be followed by a **statement**. If you want a clean jump target with no action, you can use a **null statement**:
```cpp
// ...
end:
  ; // ✅ null-statement
```
___
### 🔹 Limitations
There are two primary limitations to *jumping*:
1. You can jump only within the bounds of a single function (you can't jump outside of one function and into another).
2. You cannot jump forward to a point that skips the initialization of a variable that would still be in scope after the jump. This restriction exists to prevent you from accidentally using a variable before it has been properly constructed.

For example:
```cpp
// ...
int main() {

  goto skip;
  int x{5};
skip:
  x += 3;
  return 0;
}
```
> You can jump backwards over a variable initialization, and the variable will be re-initialized when the initialization is executed.
___
### 🔹 Avoiding `goto`
`goto` is an old but divisive feature in many programming languages, C++ included. You can check out Dijkstra's classic paper on the topic, _A Case Against the GO TO Statement_. In it, he argues that a program should be not only **syntactically correct**, but also **structurally honest**; meaning the flow of control should clearly reflect the logic the programmer intends.

He suggests that by using **induction-like patterns** (such as recursion or well-structured loops), we can more accurately represent the **dynamic process** of a program in a way that is easier to reason about. In contrast, `goto` and certain "superfluous repetition clauses" widen the gap between how code looks and how it behaves.

> Put more plainly (and less astutely than Dijkstra might), `goto` allows a programmer to jump around arbitrarily, often in ways that don’t reflect the true logic of the program.  
> That kind of unstructured control can lead to confusion, bugs, and maintenance headaches down the road.
___
### 🧠 Flashcards

What kind of scope do statement labels use?
?|?
Function scope — they're visible throughout the entire function, even before their point of declaration.

___

Can a `goto` jump across function boundaries?
?|?
No. You can only use `goto` within a single function.

___

Why must statement labels be followed by a statement?
?|?
Because the label must attach to a valid statement in the grammar; if no real code is needed, use a null statement (`;`).

___

Why does Dijkstra argue against `goto`?
?|?
Because it breaks structured control flow and creates a gap between how code looks (static structure) and how it behaves (dynamic process).

___

What happens if a `goto` skips over the initialization of a variable that's still in scope?
?|?
It’s undefined behavior and causes a compile-time error; you can't jump forward past variable initialization into its scope.


#flashcards 