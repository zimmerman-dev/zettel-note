 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚10:57 pm  📆 Thu Sep 4
 🔗 **Related Concepts**: #note #cpp [[Fundamental Data Types]] , [[Unsigned Integers]] , [[Fixed-Width Integers]]
___
## 📝 Note: Integers
--- start-multi-column: ID_gy20
```column-settings
Number of Columns: 2
Largest Column: Standard
Column Spacing: 3px
Border: off
```

An integer is an integral type that can represent a whole number—either positive, negative, or zero. In C++, there are 4 primary fundamental integer types available for use and the key difference between these various integer types is that they have varying sizes—the larger integers can hold bigger numbers (more memory).

--- column-break ---

|      Type       |   Minimum Size    |                        Note                         |
| :-------------: | :---------------: | :-------------------------------------------------: |
|   `short int`   | 2 bytes (16 bits) |                                                     |
|      `int`      | 2 bytes (16 bits) | Typically 4 bytes (32 bits) on modern architectures |
|   `long int`    | 4 bytes (32 bits) |                                                     |
| `long long int` | 8 bytes (64 bits) |                                                     |

--- end-multi-column
> 🔹 Reminder:
> - C++ only guarantees **minimum sizes** for integer types, not fixed sizes.
> - `bool` and `char` are technically **integral types**, but will be covered separately.
___
### 🔹 Signed Integers
When writing negative numbers in everyday mathematics, we use the `-` sign, i.e., `-3` means *negative 3*. And even though we typically omit the positive prefix, we know `+3` to mean *positive 3*. This attribute of being positive or negative is called the number's **sign**.

This means that when an integer is qualified with **signed** keyword, that the number's sign is stored as part of it's value. Thus, a signed integer can hold both positive and negative numbers (and 0).
#### Defining Signed Integers
```cpp
short s{};
int i{};
long l{};
long long ll{};
```
> 💡 Notice how an integer that is signed can just be written as is? This is because C++ defaults these types as signed, so you don't have to qualify the type.

Although you could write `short int`, `long int`, or `long long int`, it is preferred the short names for these type. This is because it is more typing, and it's harder to distinguish from variables of type `int`. This can lead to mistakes if the short or long modifier is inadvertently missed.

You can also use the optional *signed* keyword like this:
```cpp
signed short ss;
signed int si;
signed long sl;
signed long long sll;
```
> However, the *signed* keyword should not be used unless you need to clearly distinguish the difference.
### 🔹 Signed Integer Ranges
We learned before that a variable with `n` bits can hold `2^n` possible values. The **range**, is the set of specific values that a data type can hold. To determine the range of an integer variable, we must know two details:
- The size in bits
- Whether it is signed or unsigned ( we will discuss that below)
---
--- start-multi-column: ID_98nu
```column-settings
Number of Columns: 2
Largest Column: Left
Column Spacing: 3px
Border: off
Overflow: Hidden
```

|  Size / Type  |                            Range                            |
| :-----------: | :---------------------------------------------------------: |
| 8-bit signed  |                       `-128` to `127`                       |
| 16-bit signed |                    `-32'768` to `32'767`                    |
| 32-bit signed |             `-2'147'483'648` to `2'147'483'647`             |
| 64-bit signed | `-9'223'472'036'854'775'808` to `9'223'372'036'854'775'807` |
A table containing the ranges of signed integers of different sizes.

--- column-break ---


The formula for the range of a signed integer is: $-(2^{n-1}) \ to \ (2^{n-1})-1$

Simply plug in the size of bits for `n`.

--- end-multi-column
### 🔹 Two's Complement
Signed integers store both positive and negative values, but how does the computer know whether a value like `0000 0101` means `+5` or something else? The answer lies in how negative numbers are **encoded in binary**. **Two's Complement** is a clever trick that makes binary **subtraction work automatically**, even for negative numbers. 
#### Why Do We Need It?
With $n$ bits, we can represent $2^n$ total values.

- For **unsigned integers**, this gives a range of $0 \ to \ 2^n - 1$.
- But for **signed integers**, we need to split that range. Picture a number line like so, (..., -2, -1, 0, 1, 2, ...). Now, everything **less than** zero is the lower range, and everything **equal to and greater than** 0, is the upper part of the range. For example, with **8 bits**:
```txt
Unsigned:  0 to 255     ➡️     256 values total
Signed:  -128 to 127    ➡️     256 values total
```
> ❓ But how do you *represent* `-1` or `-128` using only `1's` and `0's`?
#### The Core Idea
In **two's complement**, the **most significant bit** (the leftmost bit) becomes the **sign bit**. Meaning, if the leftmost bit is a `0`, the number is **non-negative**. If it's `1`, the number is **negative**. This is because computers work in bits, so negative numbers can't be represented with a minus sign, it has to be stored using a special binary pattern that makes binary arithmetic work.
#### 🔹 How it Works
To turn a positive number into its negative counterpart using **two's** complement:
1. Start with the **binary version of the positive number**
2. invert all bits (flip $1s$ to $0s$, vice versa) - this is called **one's complement**
3. **Add 1** to the binary ones place.

Example: Representing $-5$ in 8-bit binary
```txt
Step 1: +5 in binary       = 0000 0101
Step 2: Invert bits        = 1111 1010
Step 3: Add 1              = 1111 1011  - this is -5
```
> So `1111 1011` means `-5` in two's complement.
#### Going Back from Two's Complement
To find the **decimal value** of a two's complement number:
1. If the first bit is `0`, it's just a normal positive number.
2. If the first bit is `1`, do the two's complement steps **in reverse**:
	1. invert the bits
	2. Add 1
	3. Then apply the minus sign

Example: What is `1111 1011`?
```txt
Step 1: Invert      |  0000 0100
Step 2: Add 1       |  0000 0101
Step 3: Add minus   |  -5
```
#### Interpreting Bit Patterns  
The exact same binary value can mean _completely different things_ depending on the type used to interpret it. For example, the bit pattern `1111 1111` is `-1` if treated as a signed 8-bit integer, but `255` if treated as an unsigned 8-bit integer. This is why the **signed or unsigned qualifier** is critical: it tells the compiler **how to interpret the bits**. The bits don’t carry meaning on their own—**the type gives them meaning**.

>💡 _Reminder:_ This is why using `int`, `unsigned int`, `short`, and so on _matters_ — even if the bits are the same, the meaning is not.

---
### 🔹 Overflow
What happens if we try to assign the value of 140 to an 8-bit signed integer? This number is outside the range that an 8-bit integer can hold. The number `140` fits in 8 bits as an unsigned value, but it **overflows the range of an 8-bit signed integer**, which only goes up to `127` due to using 1 bit for the sign.

**Overflow** - *If during the evaluation of an expression, the result is not mathematically defined or not in the range of representable values for its type, the behavior is undefined*. [^1]
- Therefore, assigning `140` to an 8-bit integer will result in undefined behavior.
```cpp
int8_t x{140}; // ❌ UB
```
> ⚠️ On some systems, this might compile and silently wrap around (e.g., 140 becomes -116). But it's still UB by the standard — don’t rely on it.
#### Caveat
When you do arithmetic in C++, **small integer types get promoted** to `int` before the operation is performed. This is called **integer promotion**, and it's part of the "usual arithmetic conversions" in C++.

Example:
```cpp
#include <iostream>
#include <cstdint>

int main()
{
	int8_t x{10};
	int8_t y{40};
	
	std::cout << x * y << '\n';
	return 0;
}
```
> Even though `x` and `y` are `int8_t`, the compiler promotes them to `int` **before** the multiplication:

Unsigned integer overflow gets covered here: [[Unsigned Integers]].
___
### 🔹 Integer Division
When dividing two integers, C++ works exactly how you'd expect when the quotient is a whole number. But when you divide a number that causes a fractional output, you will get an unexpected result unless you know what you are doing. That's because when you do **integer division, you will always get an integer result**. Since integers can't hold fractional values, the fractional part will be omitted from the output (not rounded, completely omitted).  

---
### 🧠 Flashcards

How would you figure out the range of a 5-bit signed integer?
?|?
$-(2^n)$ to $-(2^{n-1})-1$

___

What is the output?
```cpp
#include <iostream>

int main()
{
	int x = 13 / 5;
	std::cout << x;
	
	return 0;
}
```
?|?
The output would be `2` because integer division always yields an integer result.

___

What is the minimum size of a standard `int` in C++?
?|?
2 bytes (16 bits) — but typically 4 bytes on most systems today.

#flashcards 

___
[^1]: Quoted from C++20
