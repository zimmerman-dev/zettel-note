 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚10:23 pm  📆 Tue Sep 23
 🔗 **Related Concepts**: #note #cpp [[Operators - Precedence and Associativity]] , [[Fundamental Data Types]] , [[Mixed Expressions & Type Conversions & Promotion]]
___
## 📝 Note: Operators - Arithmetic, Remainder, and Exponentiation
This note is a compilation of a few different operator topics. We'll start with Arithmetic and work our way to the right. As you read this, you may get linked over to [[Operators - Basics]].
___
--- start-multi-column: ID_gq0m
```column-settings
Number of Columns: 2
Largest Column: Standard
Column Spacing: 3px
Border: off
Overflow: Hidden
```
### 🔹 Unary Arithmetic Operators  
There are two **unary** arithmetic operators, plus (`+`) and minus (`-`). Unary operators are operators that only take one operand.  
  
|  Operator   | Symbol | Form |     Operation     |
| :---------: | :----: | :--: | :---------------: |
| Unary plus  |  `+`   | `+x` |  *Value* of `x`   |
| Unary minus |  `-`   | `-x` | *Negation* of `x` |
- The **unary minus** operator returns the operand multiplied by `-1`.
- The **unary plus** operator returns the operand multiplied by `1`.
```cpp
int x = 5;
int y = -x;
// y = -x == y = -1 * 5
int z = +x;
// y = +x == y = 1 * 5
```

--- column-break ---
### 🔹 Binary Arithmetic Operators  
There are five **binary** arithmetic operators. This means each of these operators expect an **two** operands, one on each side.  
  
|    Operator    | Symbol |  Form   |              Operation              |
| :------------: | :----: | :-----: | :---------------------------------: |
|    Addition    |  `+`   | `x + y` |          `x`  *plus*  `y`           |
|  Subtraction   |  `-`   | `x - y` |          `x`  *minus*  `y`          |
| Multiplication |  `*`   | `x * y` |          `x`  *times*  `y`          |
|    Division    |  `/`   | `x / y` |        `x` *divided by* `y`         |
|   Remainder    |  `%`   | `x % y` | *remainder of* `x` *divided by* `y` |
```cpp
int x{5};
int y{3};

int addit = x + y;
int subtr = x - y;
int multi = x * y;
int divis = x / y;
int remai = x % y;
```

--- end-multi-column
___
### 🔹 Integer and Floating Point Division  
When doing division, you must consider the types for your operands. As we know (from our section on [[Floating-Point Types]], precision is the name of the game.   

- **Floating-Point Division**: Two floating point operands will give you a floating-point result. As with all floating-point numbers, rounding errors may occur.  
- **Integer Division**: Two integer operands will give you an integer result, even in the case of where the dividend can't be evenly divided by the divisor, the decimal will be truncated (dropped), not rounded.  
#### Integer division with `static_cast`  

If you have two integers that need to be divided, you can use `static_cast` to convert the integers to floating point numbers. You can either convert one or both integers using `static_cast`.  

```cpp  
#include <iostream>  
  
int main()  
{  
    constexpr int x{ 7 };  
    constexpr int y{ 4 };  
  
    std::cout << "int / int = " << x / y << '\n';  
    std::cout << "double / int = " << static_cast<double>(x) / y << '\n';  
    std::cout << "int / double = " << x / static_cast<double>(y) << '\n';  
    std::cout << "double / double = " << static_cast<double>(x) / static_cast<double>(y) << '\n';  
  
    return 0;  
}  
```  

There is no general rule of thumb; however, if you are trying to be really clear on your intent, you can convert both.  
___  
### 🔹 Dividing by 0 and 0.0  
In elementary school, you may have learned: "*Anything divided by zero is zero*". You may (or may not) have learned later--in reality, dividing by zero is much more complicated than that. And in C++, that sentiment is no different.
--- start-multi-column: ID_se6n
```column-settings
Number of Columns: 2
Largest Column: Left
Column Spacing: 3px
Border: off
Overflow: Hidden
```
#### Integer Division by 0
In C++, **dividing by zero is not legal for integer division**, and will cause either a program to crash or just UB.  
```cpp
int x{ 5 };
int y{ 0 };
int result = x / y;  // ❌ Undefined behavior!
```

C++ offers **no safety net** for integer division by zero, so you must manually check the divisor, or write in a zero check for user input:
```cpp
#include <iostream>

int main() {
  int x{10};

  std::cout << "Enter a divisor: ";
  int y{};
  std::cin >> y;

  if (y != 0)
    std::cout << "The answer is: " << x / y << '\n';
  else
   std::cout << "Cannot divide by zero!\n";
  return 0;
}
```
Look into [[Introduction to if-else]] and [[Conditionals]] for more information.

--- column-break ---
#### Floating Point Division by 0.0
Now floating point types are a tad different. It still doesn't behave like you were taught in 1st grade, but it is at least **defined behavior** if you are on a machine that follows the **IEEE-754 Standard** (most modern and even non-modern machines).

Rather than getting **UB** or a crash, these are your possible outcomes:
```cpp
 5.0 / 0.0 = +inf // Infinity
-5.0 / 0.0 = -inf // Negative infinity
 0.0 / 0.0 =  NaN // Not a number
```
While you won't crash, these may be results you are not intending, so make sure you plan accordingly.
#### TL;DR

|                        Type Category                        |        Division by `0` or `0.0` Behavior         |
| :---------------------------------------------------------: | :----------------------------------------------: |
|          **Integer types** (`int`, `short`, etc.)           |       ❌ **Undefined behavior** (may crash)       |
| **Floating-point types** (`float`, `double`, `long double`) | ✅ **Defined by IEEE-754** (returns `∞` or `NaN`) |
Look into [[Floating-Point Types]] for more information on `∞` and `NaN`.

--- end-multi-column
___
### 🔹 Arithmetic Assignment Operators

|         Operator          | Symbol |   Form   |             Operation             |
| :-----------------------: | :----: | :------: | :-------------------------------: |
|    Addition Assignment    |  `+=`  | `x += y` |        **Add** `y` to `x`         |
|  Subtraction Assignment   |  `-=`  | `x -= y` |     **Subtract** `y` from `x`     |
| Multiplication Assignment |  `*=`  | `x *= y` |        Multiply `x` by `y`        |
|    Division Assignment    |  `/=`  | `x /= y` |         Divide `x` by `y`         |
|   Remainder Assignment    |  `%=`  | `x %= y` | Put the remainder of `x/y` in `x` |
All of these operators can be thought of like this:
```cpp
x = x + y; // Addition
x = x - y; // Subtraction
x = x * y; // Multiplication
x = x / y; // Division
x = x % y; // Remainder
```
### 🔹 Modifying vs Non-Modifying Operators in C++
A **modifying operator** is one that **changes the value** stored in one of its operands. By contrast, A **non-modifying operator** just **uses the operand(s)** to compute a new value, but doesn’t change anything.
#### Non-Modifying Operators (most operators)
These **do not alter** the original variables, they just return a value.
- Examples:
```cpp
int x = 5;
int y = x + 3;    // x is still 5
int z = x * 2;    // x is still 5
bool result = (x < 10);  // x is still 5
```

|        Operator         |          Effect          |
| :---------------------: | :----------------------: |
| `+`, `-`, `*`, `/`, `%` |    compute value only    |
|  `<`, `==`, `&&`, etc.  | comparisons — no changes |
✅ These operators are **non-modifying** — they read, but don’t change, their operands.
___
#### Modifying Operators (change the left operand)
These **do change** the value stored in their **left-hand operand**.
There are two main categories:

| Operator                 | Meaning             | Modifies left operand? |
| ------------------------ | ------------------- | ---------------------- |
| `=`                      | Assign              | ✅ Yes                  |
| `+=`                     | Add and assign      | ✅ Yes                  |
| `-=`                     | Subtract and assign | ✅ Yes                  |
| `*=`                     | Multiply and assign | ✅ Yes                  |
| `/=`                     | Divide and assign   | ✅ Yes                  |
| `%=`, `<<=`, `>>=`, etc. | Bitwise + assign    | ✅ Yes                  |
Example:
```cpp
int x = 5;
x += 3;  // x is now 8
```
Here, `x + 3` doesn’t modify `x`. It just computes a value. That’s **non-modifying**.

But:
```cpp
x = 8;  // changes x!
```
Even though it _returns_ `8`, the key is:
- It **wrote that 8 to `x`’s memory location.**
___
### 🔹 Remainder Operator
The **remainder operator** (also commonly known as the **modulo operator** or **modulus operator**) is an operator that returns the remainder after doing an integer division. For example:
- `7 / 4 = 1 remainder 3`, thus `7 % 4 = 3`

Remainder is most useful when testing whether a number is evenly divisible by another number (meaning that after division, there is no remainder).
```cpp
#include <iostream>

int main() {
  int x{6};
  int y{3};

  if (x % y == 0)
    std::cout << x << " is evenly divisible by " << y << ".\n";
  else
    std::cout << x << " is NOT evenly divisible by " << y << ".\n";
  return 0;
}
```
#### Integer Remainders with Sign Rules (`+` dividend)
In C++, the remainder operator `%` is defined in a way that guarantees this identity holds: `a == (a / b) * b + (a % b)`.
- Remember, when dividing integers in the first part of the formula, the number truncates towards zero.
- In the second part, the remainder is whatever is left over dividing `a` and `b`.
```cpp
int a{7};
int b{3};

7 == (7 / 3) * 3 + (7 % 3)
7 == 2 * 3 + 1 
7 == 6 + 1
7 == 7
```
`7 / 3 = 2` due to truncation and `7 % 3` is `1` because `(2 * 3) + (1) = 7`
#### Integer Remainders with Sign Rules (`-` dividend)
When the **dividend is negative**, the remainder will also be negative. That's because remainder is always what’s left from the _original dividend_, so it keeps the same sign.
```cpp
int a{-7};
int b{3};

-7 == (-7 / 3) * 3 + (-7 % 3)
-7 ==  (-2 * 3) + (-1)
-7 ==   -6 + -1
-7 == - 7
```

This is precisely why if you flip the divisor instead:
```cpp
int a{7};
int b{-3};

7 % -3 == 1  // not -1
```
The **remainder is still positive**, because it matches the sign of the dividend (`7`), not the divisor.
___
### 🔹 Exponentiation
If you haven't already noticed, what is commonly used for exponents in math, `operator^`, is the *Bitwise XOR* operation in C++.  To do exponents in C++, you'll have to `#include <cmath>` header, and use the `pow()` function.
```cpp
#include <iostream>
#include <cmath>

int main() {
  int
}
```

### 📌 Key Definitions










___
### 🧠 Flashcards

