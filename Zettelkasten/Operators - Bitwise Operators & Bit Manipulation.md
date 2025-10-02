 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚6:14 pm  📆 Wed Oct 1
 🔗 **Related Concepts**: #note #cpp [[Operators - Overview]] , [[Boolean Logic]] , [[Hardware - Boolean Logic & Circuits (STUB)]] , [[Bit Manipulation - Overview]]
___
## 📝 Note: Operators - Bitwise Operators & Bit Manipulation
While this note _is_ about operators, it should be read as a continuation of the _bit manipulation_ series rather than an extension of [[Operators - Overview]]. The focus here is on how operators behave when applied to bit-level data. Start with [[Bit Manipulation - Overview]] for the foundation, [[Memory Management - Overview]] for details on **bits** and **bytes**, and [[Binary Numbers - Overview]] for the **binary numeral system** itself.
### 🔹 Bitwise Operators
C++ provides six bit manipulation operators, often called **bitwise operators**.

|  Operator   | Symbol |    Form    |                                     Explained                                     |
| :---------: | :----: | :--------: | :-------------------------------------------------------------------------------: |
| Left shift  |  `<<`  |  `x << n`  |   The **bits** from `x` are **shifted left** by `n` positions, new bits are `0`   |
| Right shift |  `>>`  |  `x >> n`  |  The **bits** from `x` are **shifted right** by `n` positions, new bits are `0`   |
| Bitwise NOT |  `~`   |    `~x`    |                         Each **bit** from `x` is flipped                          |
| Bitwise AND |  `&`   |  `x & y`   |  Each **bit** is **set** when **both corresponding bits** in `x` and `y` are `1`  |
| Bitwise OR  |   \|   | `x` \| `y` |   Each **bit** is set when **either corresponding bits** in `x` and `y` is `1`    |
| Bitwise XOR |  `^`   |  `x ^ y`   | Each **bit** is set when **the corresponding bits** in `x` and `y` are different. |
> *These are non-modifying operators (meaning they don't modify their operands).*
___
### 🔹 Bitwise Shifting `<<` and `>>`
First of all, **bitwise operators are defined for integral types and** `std::bitset`. To begin, lets start with how **bitwise shifting** works.
#### What is Bitwise Shifting?
In base 10, moving the decimal point left or right multiplies or divides a number by powers of 10.  
For example:
- Shift 23 one place **left**: `→ 230` (×10)
- Shift 23 one place **right**: `→ 2.3` (÷10)

This idea of “shifting” applies in binary too, but instead of powers of 10, you’re working with powers of **2**.  
That’s where **bitwise shifting** comes in.

Bitwise shifting moves the bits of a number **left** or **right** by a specified number of places. Each shift **left** multiplies the number by 2. Each shift **right** divides by 2 (dropping any remainder).
#### Syntax and Examples
So as we have seen from the table above, we use the `<<` and `>>` operators to perform bitwise shifting.
```cpp
x << n // shift bits of x left by n positions
x >> n // shift bits of x right by n positions
```

These operators work specifically on **integral types** and also with `std::bitset`. We'll start with bitsets in our examples for easy teaching.
```cpp
std::bitset<4> bin{0b0101};
```