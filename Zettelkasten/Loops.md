#### 📝 Note: Loops 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:36 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #cpp #note [[Boolean Logic]] , [[Conditionals]] , [[Increment and Decrement]] , [[Statements and Expressions]] , [[Control Flow]] , [[Loops - For | For]] , [[Loops - Ranged-based For | R-B For]] , [[Loops - While | While]] , [[Loops - Do While | Do While]]
___
## ➿ **What are Loops?**
 Loops are part of the third basic building block of programming, **iteration.** Iteration, or repetition allows the execution of a statement or block of statements repeatedly. These loops are made up of "loop conditions" and a body which contains the statements to repeat.
##### **Universal Concepts**
- **Loop Control Variable** – governs iteration and determines when the loop stops.
- **Condition** – checked each iteration to decide whether to continue.
- **Body** – the statements executed on each iteration.
##### **Common Pitfalls**
- Forgetting to update the loop control variable (can cause infinite loops).
- Using the wrong condition (off-by-one errors).
- Modifying a container incorrectly while iterating.

---
### 🎛️ **Control Statements**

- `break` – exits the loop early.
	- No further statements in the body of the loop are executed
	- Loop is immediately terminated
	- Control immediately goes to the statement following the loop construct

- `continue` – skips the rest of the current iteration and moves to the next.
	- No further statements in the body of the loop are executed
	- Control immediately goes directly to the beginning of the loop for the next iteration

- `return` – exits the entire function, not just the loop.

---

### 📚 **Loop Types**

#### [[Loops - For |For Loops]] – Controlled iteration with explicit index handling.
#### [[Loops - Ranged-based For | Ranged based For loops]] – Simplified iteration over containers.
#### [[Loops - While | While Loops]] – Runs as long as a condition is true.
#### [[Loops - Do While | Do while loops]] – Similar to while, but executes at least once.