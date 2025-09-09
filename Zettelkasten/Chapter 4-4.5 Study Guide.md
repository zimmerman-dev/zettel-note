 ♻️ Study Aid 
 ⌚8:49 pm  📆 Sun Sep 7
 🔗 **Related Concepts**: #note #quiz #cpp [[Signed Integers]] [[Unsigned Integers]] [[Fixed-Width Integers]] [[Sizeof Operator]] [[Fundamental Data Types]]
___
## 📝 Note: Chapter 4-4.5 Study Guide
###  🔹Sizes and Ranges for Integer Types
#### General Sizes for integer types

|    Type   |   Minimum Size    |   Typical Size    |
|-----------|-------------------|-------------------|
|   Short   | 2 bytes (16 bits) | 2 bytes (16 bits) |
|  Integer  | 2 Bytes (16 bits) | 4 bytes (32 bits) |
|   Long*   | 4 bytes (32 bits) | 4 bytes (32 bits) |
| Long Long | 8 Bytes (64 bits) | 8 bytes (64 bits) |

\* Long is treated differently between Windows and Mac/Linux. On Windows, **long is 4 bytes**. On Mac/Linux, **long is 8 bytes**.

#### Difference between **signed** and **unsigned** integers: 
Signed int can represent any whole number including negatives and zero, while unsigned int can only represent non-negative, whole numbers.

- Signed:   $(-2^{n-1})$ to $(2^{n-1} - 1)$  
- Unsigned: $0$ to $( 2^n) - 1$

#### Signed Integer Ranges:

|        Type        |      Minimum      |       Max         |
|--------------------|-------------------|-------------------|
|   Short (2 byte)   |      -32,768      |       32,767      |
|  Integer (4 byte)  |  -2,147,483,648   |   2,147,483,647   |
|   Long (4 byte)    |  -2,147,483,648   |   2,147,483,467   |
| Long Long (8 byte) |  $-(2^{32 - 1})$  |  $(2^{32-1})-1$   |

#### Unsigned Integer Ranges:

| Type               | Minimum | Max           |
| ------------------ | ------- | ------------- |
| Short (2 byte)     | 0       | 65,535        |
| Integer (4 byte)   | 0       | 4,294,967,295 |
| Long (4 byte)      | 0       | 4,294,967,295 |
| Long Long (8 byte) | 0       | $(2^{64})-1$  |

---
### 🔹 Signed Integer Overflow & Underflow

#### 📌 Behavior:
- **Signed overflow** (e.g., the result of adding 1 to the maximum signed int) is **undefined behavior (UB)**.
- **Signed underflow** (e.g., subtracting 1 from the minimum signed int) is also **undefined behavior (UB)**.
#### ❗ Why it matters:
- Compiler may optimize based on assumption that overflow doesn't happen.
- Can result in crashes, logic bugs, or unpredictable behavior.
#### ✅ Valid Range:
For an `n`-bit signed int:

range = $(-2^{n-1})$ to  $(2^{n-1} - 1)$
___
### 🔹 Unsigned Integer Wraparound
#### 📌 Behavior:
- **Unsigned overflow/underflow is not UB**.
- Instead, it wraps around using **modulo arithmetic**:

```cpp
 result = x mod 2^n
```

where `n` = bit width (e.g., 32 for `unsigned int`)
#### ➕➖ Example Formulas:
- Overflow:    ```
```cpp
result = (k + y) mod 2^n
```

- Underflow:
```cpp
result = (k - y) mod 2^n
```

#### 🧠 Example:
```cpp
unsigned int x = 0;
x = x - 1;  // x becomes 2^32 - 1 = 4294967295
```
---

### 🔹 Mixed Signed/Unsigned Arithmetic
#### 📌 Rule:
- In expressions mixing signed and unsigned:    
    ```
    signed → converted to unsigned before evaluation
    ```
#### ⚠️ Key Detail:
- Conversion is done using:

    ```
    unsigned_x = signed_x mod 2^n
    ```    
    even if `signed_x` is **negative**
#### 🧪 Example:
```cpp
signed int x = -1;
unsigned int y = 3;
unsigned int result = x - y;  // x → 4294967295

// result = (4294967295 - 3) mod 2^32
// result = 4294967292
```
---

### 🔹 Mixed Comparisons (Signed vs Unsigned)
#### 📌 Rule:
- Mixed comparisons convert `signed → unsigned` before comparing.
#### ⚠️ Dangerous Case:
- Comparing a **negative signed value** to an unsigned value:

    ```cpp
    int x = -1;
    unsigned int y = 3;
    
    if (x < y) // becomes: if (4294967295 < 3) → false!
    ```    
#### ✅ Best Practice:
- Avoid mixing signed and unsigned in expressions.
- Use explicit casting or stick to one type domain when possible.    
---
### ✅ Quick Reference Summary

|Case|Behavior|Formula|
|---|---|---|
|Signed Overflow/Underflow|❌ UB|N/A|
|Unsigned Overflow|✅ Wraps|`(x + y) mod 2^n`|
|Unsigned Underflow|✅ Wraps|`(x - y) mod 2^n`|
|Mixed Arithmetic|Signed → Unsigned|`signed_x mod 2^n`|
|Mixed Comparison|Signed → Unsigned|compare as unsigned|

---

### 🧠 Flashcards

#### Fundamental Types

What are **fundamental** (or **primitive**) data types in C++?
?|?
They are the **basic data** types provided by the language, like `int`, `char`, `float`, `bool`, and `void`.

---

What category of fundamental type does `char8_t` belong to?  
?|?  
**Integral** → **Character types**

---

What is the difference between **integer** and **integral** types in C++?  
?|?  
**Integer** means whole number. **Integral** means a data type _like an integer_, including `bool`, `char`, and integer types.

---

Is `enum` considered an integral type in C++?  
?|?  
❌ No — only **fundamental** types are considered integral. Enums are not.

---

What does the `_t` suffix in a type name typically signify?  
?|?  
It indicates the name is a **type alias**, usually to a specific-sized type like `int8_t`, `size_t`, etc.

---

Is `void` a fundamental data type in C++?  
?|?  
✅ Yes. It indicates the **absence of a value**.

#### Sizeof

What is the minimum size and typical size for `bool`?  
?|?  
Minimum size is 1 byte — Typical size is 1 byte.

---

What is the minimum size and typical size for `char`?  
?|?  
Minimum size is 1 byte (exactly) — Typical size is 1 byte.

---

What is the minimum size and typical size for `wchar_t`?  
?|?  
Minimum size is 1 byte — Typical size is 2 or 4 bytes.

---

What is the minimum size and typical size for `char8_t`?  
?|?  
Minimum size is 1 byte — Typical size is 1 byte.

---

What is the minimum size and typical size for `char16_t`?  
?|?  
Minimum size is 2 bytes — Typical size is 2 bytes.

---

What is the minimum size and typical size for `char32_t`?  
?|?  
Minimum size is 4 bytes — Typical size is 4 bytes.

---

What is the minimum size and typical size for `short`?  
?|?  
Minimum size is 2 bytes — Typical size is 2 bytes.

---

What is the minimum size and typical size for `int`?  
?|?  
Minimum size is 2 bytes — Typical size is 4 bytes.

---

What is the minimum size and typical size for `long`?  
?|?  
Minimum size is 4 bytes — Typical size is 4 or 8 bytes.

---

What is the minimum size and typical size for `long long`?  
?|?  
Minimum size is 8 bytes — Typical size is 8 bytes.

---

What is the minimum size and typical size for `float`?  
?|?  
Minimum size is 4 bytes — Typical size is 4 bytes.

---

What is the minimum size and typical size for `double`?  
?|?  
Minimum size is 8 bytes — Typical size is 8 bytes.

---

What is the minimum size and typical size for `long double`?  
?|?  
Minimum size is 8 bytes — Typical size is 8, 12, or 16 bytes.

---

**What does the `sizeof` operator do in C++?**  
?|?  
It returns the size (in **bytes**) of a type or object **at compile time**.

---

**How do you get the size of a variable using `sizeof`?**  
?|?  
Use `sizeof(variable)` — no need for parentheses if it’s a variable, but parentheses are fine.

---

**How do you get the size of a type using `sizeof`?**  
?|?  
Use `sizeof(Type)` — for example, `sizeof(int)` or `sizeof(MyStruct)`

---

**Can you use `sizeof` in a constant expression?**  
?|?  
✅ Yes — it’s a **constexpr** expression and can be used to define array sizes, template parameters, etc.

#### Signed Int

How would you figure out the range of a 5-bit signed integer?
?|?
$-(2^{n-1})$ to $(2^{n-1}) - 1$ 

So:

$-(2^{5-1})$ to $(2^{5-1})-1$ = -16 to 15

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

___

What is the minimum and typical size for a short integer?
?|?
2 bytes / 16 bits

---

What is the minimum and typical size for an integer?
?|?
2 bytes / 16 bits min, but typically 4 bytes / 32 bits.

---

What is the minimum and typical size for a long integer?
?|?
4 bytes / 32 bits minimum, and 4 bytes is typical for Windows systems. However, long is 8 bytes on Mac and Linux

---

What is the minimum and typical size for a long long integer?
?|?
8 bytes / 64 bits

---

Which signed integer type is guaranteed to be at least 64 bits?  
?|?  
long long int

---

Can int be larger than short on some systems?  
?|?  
Yes — int must be **≥** short in size.

---

Must long always be larger than int?  
?|?  
No — it must be **≥** int, but not necessarily larger.

---

Which header defines int16_t, int32_t, etc.?  
?|?  
`<cstdint>` (or `<stdint.h>`)

___

What is the range of an 8-bit signed integer?  
?|?  
-128 to 127

---

What is the range of a 16-bit signed integer?  
?|?  
-32,768 to 32,767

---

What is the range of a 32-bit signed integer?  
?|?  
-2,147,483,648 to 2,147,483,647

---

What is the range of a 64-bit signed integer?  
?|?  
-9,223,372,036,854,775,808 to 9,223,372,036,854,775,807

---

How do you calculate the maximum value of a signed integer type?
?|?
Use $2^{n - 1} - 1$, where $n$ is the number of bits (one bit is used for the sign)

---

Why does a signed 8-bit integer go from -128 to 127 instead of -127 to 127?  
?|?  
Because two's complement gives one more negative value than positive

#### Unsigned Int

---

What is the range of an 8-bit unsigned integer?  
?|?  
0 to 255

---

What is the range of a 16-bit unsigned integer?  
?|?  
0 to 65,535

---

What is the range of a 32-bit unsigned integer?  
?|?  
0 to 4,294,967,295

---

What is the range of a 64-bit unsigned integer?  
?|?  
0 to 18,446,744,073,709,551,615

---

What happens when an unsigned int underflows?  
?|?  
It wraps around to the maximum representable value.

---

When should you avoid unsigned types?  
?|?  
In arithmetic or loops where underflow may occur and correctness depends on sign.

#### climits

**What header provides macros like `INT_MAX` and `CHAR_BIT`?**  
?|?  
`<climits>`

---

**What does `INT_MAX` represent?**  
?|?  
The maximum value of a signed `int` (typically 2,147,483,647)

---

**What does `INT_MIN` represent?**  
?|?  
The minimum value of a signed `int` (typically −2,147,483,648)

---

**What does `CHAR_BIT` represent?**  
?|?  
The number of bits in a `char` — always at least 8

---

**What does `LONG_MAX` represent?**  
?|?  
The maximum value of a signed `long`

---

**What does `USHRT_MAX` represent?**  
?|?  
The maximum value of an **unsigned short**

___

#### cstdint

**What header defines macros like `INT32_MAX` and `UINT8_MAX`?**  
?|?  
`<cstdint>`

---

**What does `INT8_MAX` represent?**  
?|?  
The maximum value of a signed 8-bit integer (127)

---

**What does `INT16_MIN` represent?**  
?|?  
The minimum value of a signed 16-bit integer (−32,768)

---

**What does `UINT32_MAX` represent?**  
?|?  
The maximum value of an unsigned 32-bit integer (4,294,967,295)

---

**What does `INTMAX_MAX` represent?**  
?|?  
The maximum value of `intmax_t` — the largest signed integer type available

---

**What does `UINT_FAST8_MAX` represent?**  
?|?  
The max value of the fastest unsigned integer type **at least 8 bits wide**

---

**Are `INT32_MAX` and `INT32_MIN` macros or constants?**  
?|?  
They are macros — defined by the implementation based on the type's limits

#### Fixed-width

What is `std::int32_t`?  
?|?  
A typedef (alias) for a signed 32-bit integer type, guaranteed to be exactly 32 bits wide.

---

Is `std::int8_t` a new type?  
?|?  
No — it’s an alias, typically for `signed char`.

---

What header defines fixed-width integer types like `int32_t`?  
?|?  
`<cstdint>`

---

What are `int_fast32_t` and `int_least32_t`?  
?|?  
Alternative fixed-width integer aliases:

- `fast` = fastest type ≥ N bits
- `least` = smallest type ≥ N bits

---

What is `std::size_t`?  
?|?  
An unsigned integer type defined by the compiler, guaranteed to hold the size (in bytes) of any object.

---

Why is `size_t` unsigned?  
?|?  
Because sizes and indexes are never negative.

---

What does it mean when we say "`size_t` is implementation-defined"?  
?|?  
The exact type (`unsigned int`, `unsigned long`, etc.) is chosen by the compiler and may vary between systems.

---

What’s the difference between the theoretical and practical object size limits?  
?|?  
The **theoretical limit** is the max value `size_t` can represent.  
The **practical limit** is usually smaller, due to compiler/OS/memory constraints.

---

What is returned by the `sizeof` operator?  
?|?  
A value of type `std::size_t`, representing the size (in bytes) of an object or type.

---

When should you use `size_t`?  
?|?  
When counting memory, sizes, or array indexes — anywhere negative numbers don’t make sense and unsigned safety matters.


#flashcards 