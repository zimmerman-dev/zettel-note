#### 📝 Note: Conditionals 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚12:48 am  📆 Tue Jul 29
 🔗 **Related Concepts**: [[Control Flow]] , [[Operators]] , [[Boolean Logic]] , [[Loops]] , [[C++ Syntax Reference]]
___

## 📓 Selection Statements

"While statements are executed in the same order in which they appear, programs are not limited to a linear sequence of the statements." [cplusplus.com](https://cplusplus.com/doc/tutorial/control/)

#### 🔹 `If` Statements
---
```cpp title:if
if (condition) {
statement;
}
```

>-  In the syntax example above, the `condition` is the expression being evaluated and if the condition is `true`, the `statement` is executed.

>- This means, that the `if` keyword is used to execute a statement or block, *if*, and only
>- if, the condition is filled. Or simply, if the condition isn't true, the statement will be ignored.

#### 🔹 `If-Else` Statements
---
```cpp title:if-else
if (condition) {
statement_1;
} else {
statement_2;
}
```

>- Selection statements can also specify what happens when the condition is not fulfilled by using the `else` keyword to introduce an alternative path for your program logic.

>- With an `if` - `else` statement, `statement_2` is only executed when `condition` is evaluated as `false` for the first statement. In that sense, the else statement is not conditional at all.

#### 🔹 Nested  `if`-`else` Statements
---
```cpp title:Nested 
if (condition_1) {
	if (condition_1a) {
		statement_1;
	} else {
		statement_2;
	}
} else  {
	statement_1a;
}
```

>- Nesting the `if`-`else` statements allows for deeper and more conditions to be checked.

#### 🔹 `else if` Statements
---
```cpp title:Else-if
if (condition_1) {
	statement_1;
} else if (condition_2){
	statement_2;
} else {
statement_3;
}
```

>- The `else if` statement evaluates conditions by concatenating an `if` statement with an `if`-`else` statement.

>- Like a regular `if`-`else` statement, if the initial "if" condition is false, the program proceeds to check the `else if` condition. If the second condition is false, it executes the final `else` statement.

#### 🔹 `Switch` Statements
---
```cpp title:Switch
switch (integer_control_expression) {
case constant_1: statement_1; break;
case constant_2: statement_2; break;
...
case constant_n: statement_n; break;
default: statement_default;
}
```

>- The purpose of a switch statement is to check for a value among a number of possible `constant` expressions.
>- Similar to `if`-`else` statements, but limited to constant expressions.

How it works:
`switch` evaluates `integer_control_expression` and checks if it's equivalent to `constant_1`, it executes `statement_1` until it finds a `brake`                                                   



#### 🔹 Conditional (Ternary) Operator `?:`
---


- Shorthand for simple `if-else`.
- Returns a value ebased on a condition.
