 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:23 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #note #cpp [[Operators - Precedence and Associativity]] , [[Operators - Arithmetic, Remainder, and Exponentiation]] , [[Operators - Increment & Decrement]] , [[Operator Overloading]] , [[Operators - Relational & Logical]] , [[Sizeof Operator]] , [[Operators - Bitwise Operators & Bit Manipulation]]
___
## 📝 Note: Operators - Overview
An **operator** is a special symbol or keyword that performs operations on one or more operands. They're core tools within **expressions** to compute values, assign data, compare, or manipulate logic and memory.

```cpp
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
___
### 🔹 Operator Types
Operators are classified by the **number of operands** they act on:
- **Unary**: One operand, e.g. `-x`, `!flag`, `++i`
- **Binary**: Two operands, e.g. `a + b`, `x < y`, `a && b`
- **Ternary**: Three operands (only one in C++):
```cpp
condition ? expr1 : expr2
```
See also: [[Control Flow - Conditional Statements Overview]]
___
### 🔹 Arithmetic, Remainder, and Exponentiation
Covered in detail in: [[Operators - Arithmetic, Remainder, and Exponentiation]]
- Standard math: `+`, `-`, `*`, `/`, `%`
- Integer vs floating-point division
- Exponentiation uses `std::pow()` from `<cmath>` (no built-in `^` operator!)
- Beware integer truncation and signed modulo rules.
___
### 🔹 Precedence and Associativity
See: [[Operators - Precedence and Associativity]]
- **Precedence** determines which operator is evaluated first
- **Associativity** determines how operators of the same precedence group bind

> Always use parentheses for clarity in mixed expressions
___
### 🔹 Increment & Decrement
See: [[Operators - Increment & Decrement]]
- `++i` (prefix) increments _before_ use    
- `i++` (postfix) increments _after_ use    
- In complex expressions, order of evaluation matters    
- Avoid using the same variable with multiple `++` or `--` in one expression    
___
### 🔹 The Comma Operator `,`
Used to evaluate multiple expressions left-to-right; only the result of the **last** is returned.
```cpp
int x = (1 + 2, 3 + 4); // x = 7
```

Often seen in `for` loops:
```cpp
for (int i = 0, j = 10; i < j; ++i, --j)
  std::cout << i << j;
```

**Avoid** using the comma operator outside very clear use cases. It is not the same as the comma **separator** in argument lists or variable declarations.
___
### 🔹 Relational Operators
See: [[Operators - Relational & Logical]]

| Operator |           Relation           |
| :------: | :--------------------------: |
|   `>`    |         Greater than         |
|   `>=`   |     Greater or Equal to      |
|   `<`    |          Less than           |
|   `<=`   |       Less or Equal to       |
|  `<=>`   | Three-way comparison (C++20) |

Also includes:
```cpp
== // equality
!= // not equal
```

These are commonly used in conditionals and comparisons.
___
### 🔹 Logical Operators
See: [[Operators - Relational & Logical]]

| Operator |   Meaning   | Type   |
| :------: | :---------: | ------ |
|   `!`    | Logical NOT | Unary  |
|   `&&`   | Logical AND | Binary |
|    `     |             | `      |

Precedence:
- `!` > `&&` > `||`

> **Always use parentheses** to group logic clearly in expressions with multiple logical operators.
---

### 🔹 Compound Assignment Operators
These combine arithmetic/bitwise ops with assignment.

| Operator | Example |  Meaning   |
| :------: | :-----: | :--------: |
|   `+=`   | x += y  | x = x + y  |
|   `-=`   | x -= y  | x = x - y  |
|   `*=`   | x *= y  | x = x * y  |
|   `/=`   | x /= y  | x = x / y  |
|   `%=`   | x %= y  | x = x % y  |
|  `>>=`   | x >>= y | x = x >> y |
|  `<<=`   | x <<= y | x = x << y |
|   `&=`   | x &= y  | x = x & y  |
|   `^=`   | x ^= y  | x = x ^ y  |
|    `     |   =`    |     x      |
___
### 📌 Notes
- Operators are used **within expressions** to produce values or cause side effects.    
- The same symbol can have **different meanings** depending on context (e.g., `*` means multiplication _or_ pointer dereference).  
- C++ allows **operator overloading**, but this is covered later in classes.   
- Always consider **precedence and associativity** to avoid bugs in complex expressions.
___
### 🧠 Flashcards