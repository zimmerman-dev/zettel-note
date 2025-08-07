
#### 📝 Note: Operators 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:23 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #cpp #note [[Statements and Expressions]] , [[Control Flow]] , [[Pointers and References]] , [[Increment and Decrement]] , [[Boolean Logic]] , [[Conditionals]] , [[C++ Syntax Reference]]
___
### ⚙️ Operators

An **operator** is a special symbol or keyword that performs operations on one or more operands. They're the core tools used within **expressions** to compute values, assign data, compare, or manipulate logic and memory.

C++ includes a rich variety of operators, grouped by category:

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

### 🧮 Operator Types

Operators are classified by the **number of operands** they act on:

 - **Unary** - Operates on one operand:

	 - → Example: `-x`, `!flag`, `++i`

- **Binary** - Operates on two operands:
	
	- → Example: `a + b`, `x < y`, `a && b`

- **Ternary** - Operates on three operands (only one in C++):
	
	- → Example: `condition ? expr1 : expr2`
	
	- The ternary operator is the only built-in C++ operator that uses three operands—it's a compact alternative to an `if-else`.

see: [[Conditionals]]

---
## 🍻 Relational Operators

| Operator |           Relation            |
| :------: | :---------------------------: |
|   `>`    |         Greater than          |
|   `>=`   |      Greater or Equal to      |
|   `<`    |           Less than           |
|   `<=`   |       Less or Equal to        |
|  `<=>`   | Three way comparison (C++ 20) |

```cpp title:Syntax
#include <iostream>

int main() {
    int x {2};
    int y {3};

    std::cout << std::boolalpha;  // Set formatting once
    std::cout << (x > y) << std::endl; // false
    std::cout << (x < y) << std::endl; // true
    return 0;
}
```

### 📐 Testing for Equality

| Operator | Relation     |
| -------- | ------------ |
| `==`     | Equal to     |
| `!=`     | Not Equal to |

```cpp title:Syntax
expr1 == expr2 // Equals
expr1 != expr2 // Not Equals
```

### ☑️ Logical Operators

| Operator |       Relation       | Class  |
| :------: | :------------------: | ------ |
|   `!`    |  Not<br>(Negation)   | Unary  |
|   `&&`   | And<br>(Logical and) | Binary |
|   \|\|   |  Or<br>(Logical or)  | Binary |

### 🚛 Operator Precedence 

Associativity:
- Uses precedence rules when adjacent operators are different.
- Use associativity rules when adjacent operators have the same precedence. 

Precedence Hierarchy:
`! Highest precedence than ---> &&`  and   
`&& Has higher precedence than ---> ||`

Use parenthesis to absolutely remove any doubt when it comes to writing compound expressions with logical operators with more than two expressions.

```cpp title:Syntax
num1 >= 10 && num1 < 20; // and
num1 >= 10 || num1 < 20; // or
num1 >= 10 || num1 < 20;
```

- Compares the values of two expressions
- **Evaluates to a Boolean (True or False, 1 or 0)** *see [[Boolean Logic]]*
- Commonly used in [[Control Flow]] statements

### 🎱 Compound Assignment Operators

| Operator | Example | Relation   |
| -------- | ------- | ---------- |
| `+=`     | x += x  | x = x + x  |
| `-=`     | x -= x  | x = x - x  |
| `*=`     | x *= x  | x = x * x  |
| `/=`     | x /= x  | x = x / x  |
| `%=`     | x %= x  | x = x % x  |
| `>>=`    | x >>= y | x = x >> y |
| `<<=`    | x <<= y | x = x << y |
| `&=`     | x &= y  | x = x & y  |
| `^=`     | x ^= y  | x = x ^ y  |
| `\|=`    | x \|= y | x = x \| y |

---
### 💡 Notes

- Operators are used **within expressions** to produce values or cause side effects.
    
- The same symbol can have **different meanings** depending on context—e.g., `*` for both multiplication and pointer dereference.
    
- Operators obey **precedence** (who binds first) and **associativity** (who binds tighter when equal), which affect how expressions are evaluated.
    
- C++ allows **operator overloading**, meaning you can define custom behavior for operators on your own types (e.g., `+` for a `Vector3D` class).

- An **operator** is the symbol that performs the action; the **operands** are the values it acts upon.

	- `a + b   // '+' is the operator; 'a' and 'b' are the operands