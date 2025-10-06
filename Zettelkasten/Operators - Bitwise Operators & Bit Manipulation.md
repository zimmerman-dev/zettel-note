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
for example:
- Shift 23 one place **right**: `0b00010111` `→` `0b00001011` (11) 
- Shift 23 one place **left**: `0b00010111` `→` `0b00101110` (46)
#### Syntax and Examples
So as we have seen from the table above, we use the `<<` and `>>` operators to perform bitwise shifting.
```cpp
x << n // shift bits of x left by n positions
x >> n // shift bits of x right by n positions
```

These operators work specifically on **integral types** and also with `std::bitset`.
Using a bitset:
```cpp
std::bitset<4> bin{0b0101};
bin = bin << 1;
std::cout << bin << '\n'; // 1010
bin = bin >> 1;
std::cout << bin << '\n'; // 0101
```

Using and unsigned integer, then visualizing with a bitset:
```cpp
unsigned int num{8};
num = num << 1;
std::bitset<8> bin{num};
std::cout << num << " : " << bin << '\n';
```
- We start with `num = 8`.
    - In binary (8 bits): `00001000`        
- `num << 1` shifts every bit one position to the left:    
    - `00001000` → `00010000`     
- That new pattern equals decimal `16`.  

We drop it into a `bitset` to **see** the binary form:
```txt
16 : 00010000
```
___
### 🔹 Bitwise NOT `~`
Back in [[Bit Manipulation - Overview]], we used `.flip()` to invert bits in a `std::bitset`:
```cpp
std::bitset<4> bin{0b0101};
bin.flip(); // 0101 → 1010
```
The **bitwise NOT operator** `~` behaves similarly: it **flips each bit** from `0` to `1` and from `1` to `0`.

**Example:**
```
~0b0011 << → 0b1100
```
#### Important Distinction
Even though `~` and `.flip()` feel alike, there’s a major difference.
- `.flip()` only affects the bits **inside the bitset**.  
- `~` operates on the **entire width of the operand’s type**.
    
That means if you're working with a 32-bit unsigned integer, the `~` operator will flip **all 32 bits** — not just the visible portion.
```cpp

unsigned int x{4}; // 0b...00000100 (32 bits)
unsigned int y = ~x;
// y = 0b11111111111111111111111111111011
```

💡 Use `std::bitset<32>` to visualize the full result:
```cpp
std::bitset<32> binY{~x};
std::cout << binY << '\n';
```
#### What this means for Bitwise NOT
When you write:
```cpp
std::bitset<4> binX{~0b0101};
```
Here’s what really happens:
1. `~0b0101` is evaluated first.  
    - `0b0101` is an `int` literal → `0000...0101` (32 bits).      
    - Applying `~` gives `1111...1010`.        
2. That 32-bit temporary is passed into the `bitset<4>` constructor.   
    - Only the **lowest 4 bits** are kept.      
    - So `binX == 0b1010`.
```cpp
binX == 0b1010;
```
That last step — truncation to the bitset’s width — is why `~0b0101` inside `bitset<4>` ends up looking exactly like `.flip()` in this case. See: [[Logic Gates#NOT Gate `~`|NOT Truth Table]] for more details.
___
### 🔹 Bitwise OR `|`
Back in [[Operators - Relational & Logical]], we saw that **logical OR (`||`)** returns `true (1)` if either operand is true. **Bitwise OR (`|`)** works similarly, but instead of whole values, it compares **each bit** individually. It sets the result bit to `1` if **either** of the corresponding bits is `1` — otherwise, the result bit is `0`. 
#### Visual Example:
Think of it like stacking the bits:
```cpp
Operand 1 = 0b0101
// (OR |)     ↕↕↕↕
Operand 2 = 0b0110
Resulting = 0b0111
```

Now, lets use an example with some real code:
```cpp
#include <iostream>
#include <bitset>

int main() {
  unsigned x{0b0101};
  unsigned y{0b0100};
  
  std::bitset<4> bin{x | y};
  std::cout << bin << '\n';
  
  return 0;
}
```
> Output: `0101`

Here, the OR turned on an extra bit because `y` had a `1` where `x` had a `0`. See: [[Logic Gates#OR Gate ` `|OR Truth Table]] for more details.
#### When to Use `|`
**Bitwise OR** is often used when you want to set one or more specific bits to `1`, without changing the others. Common use cases include:
- **Combining bit flags** (e.g. permission settings, input states, feature toggles)
- **Turning on specific bit in a value**, regardless of it current state
___
### 🔹 Bitwise AND `&`
**Bitwise AND `&`** operates similar to **OR**, but in this case, it compares each bit in two values and sets the result bit to `1` **only if both bits are `1`**. Otherwise, the result bit is `0`. 
#### Visual Example:
Again, lets stack the bits for a clearer visualization:
```cpp
Operand 1 = 0b0101
// (AND &)    ↕↕↕↕
Operand 2 = 0b0110
Resulting = 0b0100
```

Code example:
```cpp
#include <iostream>
#include <bitset>

int main() {
  unsigned x{0b0111};
  unsigned y{0b1101};
  
  std::bitset<4> bin{x & y};
  std::cout << bin << '\n';
  
  return 0;
}
```
> Output: `0101`

**Why**?
(For both operands) Bit position 0 and 2 are both set, and bits 1 and 3 have only one flag for either operand set. See: [[Logic Gates#AND Gate `&`|AND Truth Table]] for more details.
___
### 🔹 Bitwise XOR `^`
The final bitwise operator is **bitwise XOR (`^`)**, short for **exclusive OR**.  For each pair of bits in the operands, XOR sets the resulting bit to `1` **only if the bits are different**. If both are the same (`0 0` or `1 1`), the result is `0`.
#### Visual Example:
```cpp
Operand 1 == 0b0110
// (XOR ^)
Operand 2 == 0b0011
Resulting == 0b0101
```

Code example:
```cpp
#include <iostream>
#include <bitset>

int main() {
  unsigned x{0b0110};
  unsigned y{0b1100};
  
  std::bitset<4> bin{x ^ y};
  std::cout << bin << '\n';
  
  return 0;
}
```
####  XOR with Multiple Operands
Bitwise XOR is **associative**, which means the grouping of expressions doesn’t affect the result:
```cpp
x ^ y ^ z == (x ^ y) ^ z;
```
> Even though it's tempting to think of it column-wise, **the evaluation happens pairwise**, left to right.

Code example with compound XOR:
```cpp
#include <iostream>
#include <bitset>

int main() {
  unsigned x{0b0110};
  unsigned y{0b1011};
  unsigned z{0b1111};

  std::bitset<4> bin{(x ^ y) ^ z};
  std::cout << bin << '\n';

  return 0;
}
```

What’s happening? Let’s set it up similar to the stacked view:
```cpp
Operand x == 0b0110
// (XOR ^)
Operand y == 0b1011
// (XOR ^)
Operand z == 0b1111
Resulting == 0b0010 
```
> How does this work? Let’s break it down step by step:

```cpp
Operand x == 0b0110
// ^
Operand y == 0b1011
resulting == 0b1101
// ^
Operand z == 0b1111
final res == 0b0010
```
📌 Even though the truth table rule says “odd number of 1s = 1”, the evaluation still happens **pairwise**, one step at a time.
### 🔹 Bitwise Assignment Operators
Similar to the arithmetic assignment operators, C++ provides bitwise assignment operators. **These do modify the left operand**.

|  Operator   | Symbol |    Form     | Form Extended  |              The operation modifies the left operand where:              |
| :---------: | :----: | :---------: | :------------: | :----------------------------------------------------------------------: |
| Left Shift  |  `<<`  |  `x <<= n`  |  `x = x << n`  |   The bits in `x` are shifted left by `n` positions, new bits are `0`    |
| Right Shift |  `>>`  |  `x >>= n`  |  `x = x >> n`  |   The bits in `x` are shifted right by `n` positions, new bits are `0`   |
| Bitwise AND |  `&`   |  `x &= y`   |  `x = x & y`   |   Each bit is set when both corresponding bits in `x` and `y` are `1`    |
| Bitwise OR  |   \|   | `x` \|= `y` | `x = x` \| `y` |  Each bit is set when either corresponding bits in `x` and `y` are `1`   |
| Bitwise XOR |  `^`   |  `x ^= y`   |  `x = x ^ y`   | Each bit is set when the corresponding bits in `x` and `y` are different |
___
### 🧠 Flashcards

What does the bitwise OR operator `|` do to each pair of bits?  
?|?  
It sets the result bit to `1` if either of the bits is `1`; otherwise, it sets it to `0`.

---

What’s the output of this expression? `0b0101 | 0b0011`  
?|?  
`0b0111`

---

Which bit falls off in a 4-bit left shift: bit 0 or bit 3?  
?|?  
Bit 3 (the leftmost bit)

---

What’s the result of `0b1101 & 0b0111`?  
?|?  
`0b0101`

---

How does `bitset<4> bin = ~0b0101;` behave?  
?|?  
The `~` flips all 32 bits, but `bitset<4>` truncates it to the lowest 4 bits: `0b1010`.

---

Which operator would you use to toggle a single bit: `&`, `|`, or `^`?  
?|?  
`^` (XOR toggles the bit)

---

What does this do? `flags |= (1 << 2);`  
?|?  
It sets bit 2 of `flags` to `1`, without changing other bits.

---

How is `x ^= y` different from `x = x ^ y`?  
?|?  
It’s not — they’re functionally equivalent. `^=` is shorthand.

---

In a compound XOR like `x ^ y ^ z`, how is it evaluated?  
?|?  
Pairwise, left to right: `(x ^ y) ^ z`

---

True or False: `bitset<4> bin = bin << 1;` modifies `bin` in-place.  
?|?  
False — `bin << 1` returns a new bitset; use `bin <<= 1` for in-place shift.

#flashcards 