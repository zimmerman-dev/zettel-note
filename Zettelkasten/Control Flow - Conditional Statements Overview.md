 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚12:48 am  📆 Tue Jul 29
 🔗 **Related Concepts**: #note #cpp [[Control Flow - If Statement - Basics]] , [[Control Flow - If Statement - Advanced]] , [[Operators - Relational & Logical]]
___
## 📝 Note: Control Flow - Conditional Statements Overview
_"While statements are executed in the same order in which they appear, programs are not limited to a linear sequence of the statements."_ – [cplusplus.com](https://cplusplus.com/doc/tutorial/control/)

--- start-multi-column: ID_13jx
```column-settings
Number of Columns: 3
Largest Column: Standard
Column Spacing: 3px
Border: off
Overflow: Hidden
```
### 🔹`if`
```cpp
if (condition) {
    statement;
}
```

> The `if` keyword executes a statement or block **only if the condition is true**.  
> If the condition is false, the block is skipped and the program continues.

--- column-break ---
### 🔹`else` 
```c
if (condition) {
    statement_1;
} else {
    statement_2;
}
```

> The `else` keyword provides an **alternative path** if the initial condition is false.  
> In an `if-else`, **exactly one** of the two blocks executes.

--- column-break ---
### 🔹`else if` 
```c
if (condition_1) {
    statement_1;
} else if (condition_2) {
    statement_2;
} else {
    statement_3;
}
```

> The `else if` construct chains multiple conditions together.  
> If the first condition is false, the program checks the next `else if`, and finally executes the `else` block if none match.

--- end-multi-column
See: [[Control Flow - If Statement - Basics]], then: [[Control Flow - If Statement - Advanced]] 
___
### 🔹 `switch` Statements
```c
switch (control_expression) {
    case constant_1:
        statement_1;
        break;
    case constant_2:
        statement_2;
        break;
    // more cases...
    default:
        statement_default;
}
```

> A `switch` compares an **integral or enumeration** expression against a set of constant values.  
> It is often clearer than using many `else if` statements when testing the same variable.

**Key Points**:

- Each `case` label must be a **constant expression**.
- Use `break` to prevent **fall-through** (execution continuing into the next case).
- The `default` label is optional, but serves as a catch-all.

**Example of intentional fall-through**:

```c
switch (x) {
    case 1:
    case 2: // falls through from case 1
        std::cout << "x is 1 or 2";
        break;
}
```

See: [[Control Flow - If Statement Alternatives]]
___
### 🔹 Conditional (Ternary) Operator `?:`
```c
(condition) ? expr_1 : expr_2;
```

> The ternary operator is a compact alternative to `if-else`.  
> It evaluates `condition` and returns:
> 
> - `expr_1` if true
> - `expr_2` if false

> Best used for **simple expressions**. For complex logic, stick to full `if-else` for clarity.
___
