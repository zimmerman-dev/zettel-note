 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:23 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #note #cpp [[Data Types]], [[Boolean Logic]], [[Statements and Expressions]]
___
## 📝 Note: Literals & Operators
### 🔹 Literals
Consider the following two statements:
```cpp
std::cout << "Hello world!";
int x { 5 };
```
> `"Hello world!"` is a **string literal**, and `5` is an **integer literal**.  
`x` is **not** a literal — it’s a variable initialized **with** a literal. // NEW clarification
### 🔹 Key insight
- Literals are values that are inserted directly into the source code. These values usually appear directly in the executable code (unless they are optimized out).
- Objects and variables represent memory locations that hold values. These values can be fetched on demand.
### 🔹 Types of Literals

|**Type**|**Example**|**Description**|
|---|---|---|
|Integer|`42`, `-7`, `0xFF`|Whole numbers (decimal, hex, octal, binary)|
|Floating-point|`3.14`, `-0.5f`|Decimal numbers with fractions|
|Boolean|`true`, `false`|Logical truth values|
|Character|`'A'`, `'\n'`|Single characters|
|String|`"Hello"`, `"Hi\n"`|Sequences of characters|

---
### 🔹 Operators
An **operator** is a special symbol or keyword that performs operations on one or more operands. They're the core tools used within **expressions** to compute values, assign data, compare, or manipulate logic and memory.

```cpp title:Operators
/*==========================================================================*/
+     // Arithmetic: addition
-     // Arithmetic: subtraction
*     // Arithmetic: multiplication
/     // Arithmetic: division
%     // Arithmetic: modulo
/*==========================================================================*/
=     // Assignment
==    // Equality comparison
!=    // Inequality comparison
< >   // Relational operators
/*==========================================================================*/
&&    // Logical AND
||    // Logical OR
!     // Logical NOT
/*==========================================================================*/
++    // Increment
--    // Decrement
/*==========================================================================*/
&     // Bitwise AND or address-of (context matters)
*     // Pointer dereference or multiplication
->    // Member access via pointer
.     // Member access via object
/*==========================================================================*/
```
### 🔹 Operator Types
Operators are classified by the **number of operands** they act on:
 
- **Unary** → One operand: `-x`, `!flag`, `++i`   
- **Binary** → Two operands: `a + b`, `x < y`, `a && b`
- **Ternary** → Three operands (only one in C++):
```cpp
condition ? expr1 : expr2
```

see: [[Conditionals]]
___
## 🍻 Relational Operators

| Operator |           Relation            |
| :------: | :---------------------------: |
|   `>`    |         Greater than          |
|   `>=`   |      Greater or Equal to      |
|   `<`    |           Less than           |
|   `<=`   |       Less or Equal to        |
|  `<=>`   | Three way comparison (C++ 20) |

### 🔹 Testing for Equality
```cpp title:Syntax
expr1 == expr2 // Equals
expr1 != expr2 // Not Equals
```
---
### 🔹 Logical Operators

| Operator |       Relation       | Class  |
| :------: | :------------------: | ------ |
|   `!`    |  Not<br>(Negation)   | Unary  |
|   `&&`   | And<br>(Logical and) | Binary |
|   \|\|   |  Or<br>(Logical or)  | Binary |
### 🔹 Operator Precedence 
Associativity rules decide which side binds first when operators share precedence:
- `!` > `&&` > `||`
- Always use **parentheses** when mixing logical operators — it avoids surprises.
### 🔹 Compound Assignment Operators

| Operator | Example |  Relation  |
| :------: | :-----: | :--------: |
|   `+=`   | x += x  | x = x + x  |
|   `-=`   | x -= x  | x = x - x  |
|   `*=`   | x *= x  | x = x * x  |
|   `/=`   | x /= x  | x = x / x  |
|   `%=`   | x %= x  | x = x % x  |
|  `>>=`   | x >>= y | x = x >> y |
|  `<<=`   | x <<= y | x = x << y |
|   `&=`   | x &= y  | x = x & y  |
|   `^=`   | x ^= y  | x = x ^ y  |
|  `\|=`   | x \|= y | x = x \| y |

---
### 🔹 Notes
- Operators are used **within expressions** to produce values or cause side effects.
- The same symbol can have **different meanings** depending on context—e.g., `*` for both multiplication and pointer dereference.
- Operators obey **precedence** (who binds first) and **associativity** (who binds tighter when equal), which affect how expressions are evaluated.
- C++ allows **operator overloading**, meaning you can define custom behavior for operators on your own types (e.g., `+` for a `Vector3D` class).
- An **operator** is the symbol that performs the action; the **operands** are the values it acts upon.
	- `a + b   // '+' is the operator; 'a' and 'b' are the operands
---
### 📌 Key Definitions
- **Literal** → A fixed value written directly in code, e.g. `42` or `"hello"`.
- **Variable** → A named storage location holding a value.
- **Operator** → A symbol or keyword that performs an operation on operands.
- **Operand** → The value or variable an operator acts on.
- **Expression** → Combines literals, variables, and operators to produce a value.
- **Statement** → A complete instruction; often contains expressions.
---
### 🧠 Flashcards
What is a literal?|||A hardcoded value written directly in the source code. 

Variables store values, literals **ARE** their values. 

What’s the difference between an operator and an operand?|||Operators act on operands.  

What's the ternary operator used for?|||A shorthand conditional: `condition ? expr1 : expr2` 

Which has higher precedence, `&&` or `||`? |||`&&` binds tighter. Use parentheses when mixing. 
#flashcards 
