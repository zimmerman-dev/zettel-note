 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚10:23 pm  📆 Tue Sep 23
 🔗 **Related Concepts**: #note #cpp [[Operators - Precedence and Associativity]] , [[Fundamental Data Types]] , [[Type Conversion - Overview]]
___
## 📝 Note: Operators - Arithmetic, Remainder, and Exponentiation
This note is a compilation of a few different operator topics. We'll start with Arithmetic and work our way to the right. As you read this, you may get linked over to [[Operators - Overview]].
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
Look into [[Control Flow - If Statement - Basics]] and [[Control Flow - Conditional Statements Overview]] for more information.

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
In mathematics, the caret symbol (`^`) typically means exponentiation (e.g. `2^3 = 8`).  
However, in C++, `^` is the **bitwise XOR** operator, _not_ exponentiation.

To perform exponentiation in C++, use the `std::pow()` function from the `<cmath>` header:
```cpp
#include <iostream>
#include <cmath>

int main() {
  double product{ std::pow(5.0, 3.0) };
  std::cout << product << '\n';

  return 0;
}
```

**Note**: `std::pow()` works with floating-point types. If you need to perform exponentiation on integers (e.g. `2^5 = 32`) without converting to double, it’s better to write your own integer-based version:
```cpp
#include <iostream>

int intPow(int base, int exponent) {
  int product{ 1 };
  for (int i = 0; i < exponent; ++i) {
    product *= base;
  }
  return product;
}

int main() {
  int product{ intPow(2, 5) };
  std::cout << product << '\n';
  return 0;
}
```
**Note**: This basic version doesn't handle edge cases like negative exponents or overflow. For robust usage, you’d want to:

-   Validate input (e.g. no negative exponents unless using `double`)  
-   Consider using `std::int64_t` for large bases   
-   Possibly switch to `constexpr` if you're doing compile-time powers
___
### 🧠 Flashcards

What type of operator is `x += 3` and why is it classified that way?  
?|?  
A modifying operator — because it changes the value stored in the left-hand operand (`x` is updated).

---

If `int a = -7; int b = 3;`, what is the value of `a % b` in C++?  
?|?  
`-1`, because the remainder keeps the sign of the dividend (`a`), even if the divisor is positive.

---

Will this compile?
```cpp
int x{2};
int y{5};

int result{std::pow(x,y)};
```  
?|?  
Yes, it will compile — but `std::pow(x, y)` returns a `double`, so the result will be **narrowed** when initializing `int result`, which may cause a **compiler warning** or **truncation**. For pure integer math, write your own function instead.

---

In C++, what happens when you divide a floating-point number by 0.0? (e.g., `5.0 / 0.0`)  
?|?  
It returns positive or negative infinity (or NaN for 0.0/0.0), as defined by IEEE-754.

---

What value does `int result = 7 / 4;` store in `result` and why?  
?|?  
`1` — because both operands are integers, so the result is truncated (not rounded).

---

What is the behavior of `7 % -3` in C++ and why?  
?|?  
It returns `1` — the sign of the remainder always matches the dividend (`7`), not the divisor.

---

What is the general identity rule that the remainder operator `%` must follow in C++?  
?|?  
`a == (a / b) * b + (a % b)`

---

What kind of operator is the unary minus (e.g., `-x`), and what does it actually do?  
?|?  
A unary arithmetic operator — it negates the value, equivalent to multiplying by -1.

---

Why is `int x = 5; int y = x * 2;` considered non-modifying?  
?|?  
Because the expression computes a new value but doesn't change `x`; it only uses `x`.

---

How would you rewrite `x *= y;` without using the shorthand operator?  
?|?  
`x = x * y;`


#flashcards 