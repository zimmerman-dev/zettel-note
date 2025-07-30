#### 📝 Note: Conditionals 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚12:48 am  📆 Tue Jul 29
 🔗 **Related Concepts**: [[Control Flow]] , [[Operators]] , [[Boolean Logic]] , [[Loops]] , [[C++ Syntax Reference]]
___
Alters flow based on **conditions**.

## 📓 If Statements 


🔹 `If` Statements
- Execute a block **only if** a condition is true.
```cpp title:if
if (condition) {
statement;
}
```

🔹 `If-Else` Statements
- Choose between **two paths** based on a condition.

```cpp title:if-else
if (condition) {
statement;
} else {
statement;
}
```

🔹 Nested `if`'s and `if`-`else`'s
- Nesting the allows for deeper and more conditions to be checked.
```cpp title:Nested 
if (condition) {
	if (condition) {
		{statement;
		} else {
		statement;}
	} else {
	statement}
}
```


🔹 Switch Statements
- Multi-way branching based on the value of an expression.
- Often used instead of multiple `if-else` chains.

🔹 Conditional (Ternary) Operator `?:`
- Shorthand for simple `if-else`.
- Returns a value based on a condition.
