 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚6:41 pm  📆 Sun Sep 7
 🔗 **Related Concepts**: #note #cpp [[Binary Numbers & Bit Manipulation]] [[Signed Integers]] [[Fundamental Data Types]] [[Memory Management - Basics]]
___
## 📝 Note: Unsigned Integers
--- start-multi-column: ID_gy20
```column-settings
Number of Columns: 2
Largest Column: Standard
Column Spacing: 3px
Border: off
```
### 🔹 Defining Unsigned Integers
**Unsigned Integers** are integers that can only hold non-negative, whole numbers.

```cpp
unsigned short us;
unsigned int ui;
unsigned long ul;
unsigned long long ull;
```
--- column-break ---
### 🔹 Unsigned Integer Ranges
An $n$-bit unsigned variable has a range of $0 \ to \ (2^n)-1$.

|   Size / Type   |                Range                |
| :-------------: | :---------------------------------: |
| 8-bit unsigned  |            `0` to `255`             |
| 16-bit unsigned |           `0` to `65,535`           |
| 32-bit unsigned |       `0` to `4'294'967'295`        |
| 64-bit unsigned | `0` to `18'446'744'073'709'551'615` |
When no negative numbers are required, unsigned integers are well-suited for networking and systems with little memory, because unsigned integers can represent a higher range of positive numbers using the same amount of memory.

--- end-multi-column
### 🔹 Unsigned Integer "Overflow"
**Overflow** in [[Signed Integers]] results in **undefined behavior**, but what happens if you exceed the range of unsigned integer?  

Unsigned integers in C++ do **not** exhibit undefined behavior on overflow. Instead, they **wrap around** using **modulo arithmetic**. That means if you exceed the maximum value of an unsigned type, the result "loops back" around to the beginning of its range:

Example:
```cpp
#include <iostream>

int main()
{
	unsigned short x{65535};
	x = x + 1;
	
	std::cout << x;
	return 0;
}
```
> The output would be `0`, because once `x` exceeds the maximum value of the `unsigned short` range (65535), it wraps around to `0`. In this case, it was just 1 over.
>💡 Unsigned overflow is _well-defined_ in the C++ standard and always wraps modulo `2^n`.

You can also think of it this way:

*"If I overflow past the max by `n`, I’ll land on value `n - 1`."*
___
### 🔹 An Aside
Quote from [LearnCpp Chapter 4.5]([4.5 — Unsigned integers, and why to avoid them – Learn C++](https://www.learncpp.com/cpp-tutorial/unsigned-integers-and-why-to-avoid-them/)

*"Many notable bugs in video game history happened due to wrap around behavior with unsigned integers. In the arcade game Donkey Kong, it’s not possible to go past level 22 due to an overflow bug that leaves the user with not enough bonus time to complete the level.*

*In the PC game Civilization, Gandhi was known for often being the first one to use nuclear weapons, which seems contrary to his expected passive nature. Players had a theory that Gandhi’s aggression setting was initially set at 1, but if he chose a democratic government, he’d get a -2 aggression modifier (lowering his current aggression value by 2). This would cause his aggression to overflow to 255, making him maximally aggressive! However, more recently Sid Meier (the game’s author) clarified that this wasn’t actually the case."*
___
### 🔹 The Unsigned Integer Controversy
Many developers (and some large development firms, such as Google) believe that developers should generally avoid unsigned integers. This is largely to do with two behaviors that can cause problems.

1. With signed integers, it actually takes a little effort to accidentally overflow the top or bottom of the range because those values are far from 0. With unsigned integers, it is a lot easier to trigger wrap-around at the bottom of the range because it's 0, which is close to where the majority of our values are. This is what's called  unsigned integer **underflow**.

**Example:**
```cpp
#include <iostream>

// assume int is 4 bytes
int main()
{
	unsigned int x{ 2 };
	unsigned int y{ 3 };

	std::cout << x - y << '\n'; // prints 4294967295 (incorrect!)

	return 0;
}
```
> This is an obvious mistake, but consider what would happen if you had a while loop using an unsigned variable that decrements past 0?

2. Here is another example of where things can go wrong:
```cpp
#include <iostream>

// assume int is 4 bytes
int main()
{
    signed int s { -1 };
    unsigned int u { 1 };

    if (s < u) // -1 is implicitly converted to 4294967295, and 4294967295 < 1 is false
        std::cout << "-1 is less than 1\n";
    else
        std::cout << "1 is less than -1\n"; // this statement executes

    return 0;
}
```
> We will cover this more in [[Arithmetic Conversions(STUB)]]
####  Best Practices
Favor signed numbers over unsigned numbers for holding quantities (even quantities that should be non-negative) and mathematical operations. Avoid mixing signed and unsigned numbers.
___
### 🔹 So When?
Unsigned integers have their place, especially in lower level, and systems level programming. We will talk more about that in [[Binary Numbers & Bit Manipulation]]. Also, unsigned integers are sometimes relatively unavoidable, mainly when it comes to array indexing. We'll talk more about that in [[Arrays]]. Lastly, in embedded systems or memory-constrained environments, unsigned integers are often necessary due to hardware constraints or to avoid wasted space.
___
### 📌 Key Definitions
- **Unsigned Integer**  
    An integer type that can represent only non-negative whole numbers in the range `0` to `(2^n - 1)` where `n` is the number of bits.

- **Unsigned Overflow**  
    A condition where the result of an unsigned arithmetic operation exceeds the maximum representable value and **wraps around** using modulo arithmetic, starting again from zero.

- **Unsigned Underflow**  
    A special case of overflow where subtracting from an unsigned value causes it to wrap around to the **top** of its range (e.g., `0 - 1` becomes the maximum representable value).

- **Implicit Type Conversion**  
    When C++ automatically promotes or converts one operand to match another in an expression. Mixing signed and unsigned types can produce surprising results due to this conversion.
___
### 🧠 Flashcards

**What is the range of a 16-bit unsigned integer?**  
?|?  
`0` to `65,535` (`2^16 - 1`)

___

**What happens if you assign `65536` to a `uint16_t`?**  
?|?  
It wraps around to `0` (65536 mod 2^16 = 0)

---

**What is the output?**

```cpp
#include <iostream>
int main() 
{
     unsigned short x{65535};
     x = x + 5;
     std::cout << x << '\n';
}
```
?|?  
`4` → The value wraps around: 65535 + 5 = 65540, 65540 mod 65536 = 4

---

**What is the output?**

```cpp
#include <iostream>
int main() 
{     
	unsigned int x{2};     
	unsigned int y{3};     
	std::cout << x - y << '\n';
}
```
?|?  
`4294967295` (on a 32-bit `unsigned int`) — wraps around due to underflow

---

**Why should you avoid mixing signed and unsigned types in expressions?**  
?|?  
Because C++ promotes the signed value to unsigned, which may cause unexpected results, such as `-1 < 1` evaluating to false.
