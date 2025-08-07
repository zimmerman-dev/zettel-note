#### 📝 Note: Statements and Expressions 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:26 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #cpp #note [[C++ Syntax Reference]] , [[Operators]] , [[Functions]] , [[Loops]] , [[Conditionals]]
___
### 🔣 Expressions

At it's core, an **expression** is most basic building blocks of a program—a sequence of **operands** and **operators** that evaluates to a value.

Expressions can be as simple as a *literal* or as complex as chain of operations. They're used to compute values, assign data, or make decisions.

```cpp title:Expressions
34                   // Literal expression (evaluates to 34)
fav_num         // Variable Expression (eval's to the value stored in fav_num)
1.5 + 2.8            // Addition Expression (eval's to 4.3)
2 * 5                // Multiplication Expression (eval's to 10)
a < b                // Relational Expression (eval's to true or false)
a = b                // Assignment Expression (assigns b to a, returns the value of a)
```

###  💡 Notes

- Every expression **produces a value**.
- Even the assignment expression `a = b` yields the value assigned.
- Expressions **can also have side-effects**, especially assignments or function calls.

---
###  🧾 Statements

A statement is a complete instruction that tells the computer to do something. In C++, a statement is terminated with a semicolon (`;`) and often contains expressions.

C++ includes many types of statements:

|         **expression**         |    **null**     |         **compound**         | **selection** (`if`, `switch`) | **try-catch blocks** |
| :----------------------------: | :-------------: | :--------------------------: | :----------------------------: | :------------------: |
| **iteration** (`for`, `while`) | **declaration** | **jump** (`break`, `return`) |  **jump** (`break`, `return`)  |                      |

```cpp title:Statements
int x;                             // Declaration Statement
fav_num = 12;                      // Assignment (expression) statement
1.5 + 2.8;                         // Expression statement
x = 2 * 5;                         // Assignment w/ arithmetic statement
if (a > b) std::cout << "a > b";   // Selection (conditional) statement  
for (int i = 0; i < 10; i++) {};      // Iteration statement
```

---

### 💡 Notes

- A statement may contain expression(s), but not all expressions are statements.
-  Compound statements are blocks enclosed in `{}` that group multiple statements together.
- Some statements, like `1.5 + 2.8`; , are valid but pointless if their result isn't used. They evaluate but produce no side-effects.