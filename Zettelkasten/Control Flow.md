♻️ (*MinGW, Windows11, Codelite*)   
 ⌚8:04 pm  📆 Mon Jul 28
 🔗 **Related Concepts**: #note #cpp [[Loops - Overview]], [[Conditionals]], [[Jump Statements]]
___
## Control Flow
- The **order** in which individual statements, instructions, or function calls are executed.
- In C++, there are **three primary structures** of control flow:
## Big Ideas
### 🔹 Sequence
- **Default** flow of a program: statements execute **top to bottom**.
- Example: variable declarations, assignments, function calls in order.

---
### 🔹 Selection (Decision-Making)
- Alters flow based on **conditions**.

**If Statements**
- Execute a block **only if** a condition is true.

**If-Else Statements**
- Choose between **two paths** based on a condition.

**Switch Statements**
- Multi-way branching based on the value of an expression.
- Often used instead of multiple `if-else` chains.

**Conditional (Ternary) Operator** `?:`
- Shorthand for simple `if-else`.
- Returns a value based on a condition.

see: [[Conditionals]]
___
### 🔹 Iteration (Loops)
- Repeats a block of code **while** or **until** a condition is met.
#####  [[Loops - For]]
- Used when the number of iterations is known or count-controlled.
#####  [[Loops - While]]
- Used when the condition is checked **before** each iteration.
#####  [[Loops - Do While]]
- Similar to `while`, but the condition is checked **after** the first iteration (executes at least once).