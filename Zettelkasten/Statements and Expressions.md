 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:26 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #note #cpp [[C++ Syntax Reference]], [[Operators - Overview]]
___
## 📝 Note: Statements and Expressions
###  🔹Expressions
At it's core, an **expression** is most basic building blocks of a program—a sequence of **operands** and **operators** that evaluates to a value.

Expressions can be as simple as a *literal* or as complex as chain of operations. They're used to compute values, assign data, or make decisions.

```cpp title:Expressions
34                   // Literal expression (evaluates to 34)
fav_num              // Variable Expression (eval's to the value stored in fav_num)
1.5 + 2.8            // Addition Expression (eval's to 4.3)
2 * 5                // Multiplication Expression (eval's to 10)
a < b                // Relational Expression (eval's to true or false)
a = b                // Assignment Expression (assigns b to a, returns the value of a)
```
####   Notes
- Every expression **produces a value**.
- Even the assignment expression `a = b` yields the value assigned.
- Expressions **can also have side-effects**, especially assignments or function calls.

---
###   🔹Statements
A statement is a complete instruction that tells the computer to do something. In C++, a statement is the smallest unit of computation in C++, and they're terminated with a semicolon (`;`). Often contains expressions.

C++ includes many types of statements:

|         **expression**         |    **null**     |         **compound**         | **selection** (`if`, `switch`) | **try-catch blocks** |
| :----------------------------: | :-------------: | :--------------------------: | :----------------------------: | :------------------: |
| **iteration** (`for`, `while`) | **declaration** | **jump** (`break`, `return`) |  **jump** (`break`, `return`)  |                      |

```cpp title:Statements
int x;                              // Declaration Statement
fav_num = 12;                       // Assignment (expression) statement
1.5 + 2.8;                          // Expression statement
x = 2 * 5;                          // Assignment w/ arithmetic statement
if (a > b) std::cout << "a > b";    // Selection (conditional) statement  
for (int i = 0; i < 10; i++) {};    // Iteration statement
```

---
#### Notes
- A statement may contain expression(s), but not all expressions are statements.
-  Compound statements are blocks enclosed in `{}` that group multiple statements together.
- Some statements, like `1.5 + 2.8`; , are valid but pointless if their result isn't used. They evaluate but produce no side-effects.
---
### 📌 Key Definitions
1. Statement: A statement is a complete instruction that tells the computer to do something and they're terminated with a semicolon.
2. Expression: An expression is a fragment of code, with operators and operands, the evaluates to a value. i.e., `1 * 2`
3. Assignment: The act of storing a value into an already declared and defined variable. 
4. Declaration: Informs the system about the existence of an entity (name and type) and how it should be handled.
5. Definition: Provides the complete details of an entity, including implementation or initial value and typically allocates memory (initialization).
6. Initialization: A definition that gives an entity it's first value.
---
### 🧠 Flashcards
- What is an *Expression*?|||An expression is fragment of code -- a sequence of operators and operands -- that evaluate to a value. 

- What is a *Statement*?|||A statement is an instruction that causes the program to perform some action. 

- Every expression produces a ==value==. 

- `int x;` is what type of statement?|||Declaration statement (also a definition, since it allocates storage). 

- `num = 5;` is what type of statement?|||Assignment statement. 

- `int num = 5;` is both definition and declaration. What else is it and what is it's purpose?|||An initialization and it's purpose is to inform the program the name and type of an entity and allocate memory. 

- `"Hello"` is a ==literal== expression. 

- What is the difference between `23 + 45` and `23 + 45;`?|||The first block is an expression and the second block is an expression statement. 
#flashcards