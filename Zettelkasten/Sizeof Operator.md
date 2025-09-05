 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚9:32 pm  📆 Thu Sep 4
 🔗 **Related Concepts**: #note #cpp
___
## 📝 Note: Sizeof Operator
In [[Fundamental Data Types]], we introduced how memory on modern machines is typically organized into **byte-sized** units, with each unit assigned a unique address. We imagined each unit as a small, 1-byte "box" labeled with an address, used to store and retrieve data.

But in reality, it's a bit more complex.

If you’ve been paying attention, you’ll notice we’ve been storing and accessing objects that are **clearly larger than 1 byte**. A single object might occupy 1, 2, 4, or even more consecutive memory addresses, and we can infer that the amount of memory an object uses is **based on its data type**.

Because we usually interact with memory through variable names, this underlying complexity is often hidden from us, for better or worse.
### 🔹 Bits Recap
To summarize, an object with *n* bits (where n is an integer) can hold `2^n` unique values. Therefore, a byte-sized object can hold `2^8` different value.
--- start-multi-column: ID_ge8h
```column-settings
Number of Columns: 3
Largest Column: Right
Column Spacing: 3px
Border: off
```

| Bit 0 |
| :---: |
|   0   |
|   1   |
A Single bit can hold **two** possible value, either `0`, or `1`. `2^1`.

--- column-break ---

| Bit 0 | Bit 1 |
| :---: | :---: |
|   0   |   0   |
|   0   |   1   |
|   1   |   0   |
|   1   |   1   |
2 bits can hold **four** possible value, `2^2`.

--- column-break ---

| Bit 0 | Bit 1 | Bit 2 |
| :---: | :---: | :---: |
|   0   |   0   |   0   |
|   0   |   0   |   1   |
|   0   |   1   |   0   |
|   1   |   0   |   0   |
|   1   |   0   |   1   |
|   1   |   1   |   0   |
|   1   |   1   |   1   |
3 bits can hold **eight** possible values, `2^3`.

--- end-multi-column
_____
### 🔹 Fundamental Data Types - Sizes
The next question is, *How much memory do objects of any given fundamental data type use*? We know that the **smallest addressable unit** in C++ is a byte, but what other _rules_ govern the size of an object?

- An object must occupy at least **1 byte** (so that each object has a distinct memory address).
- A byte must be at least **8 bits**.
- The integral types `char`, `short`, `int`, `long`, and `long long` have a minimum size of 8, 16, 32, and 64 bits respectively.
- `char` and `char8_t` are exactly 1 byte (at least 8 bits).

> 💡 When we talk about the **size** of a type, we really mean the size of an instantiated object of that type.

--- start-multi-column: ID_ojna
```column-settings
Number of Columns: 2
Largest Column: Standard
Column Spacing: 3px
Border: off
```

### 🔹 Stipulations 
- A byte is 8 bits.
- Memory is byte addressable (we can access every byte of memory independently).
- Floating point support is IEEE-754 compliant.
- We are on a 32-bit or 64-bit architecture.

Given the above assumptions, we can reasonably state the following:

--- column-break ---

|    Category    |       Type       |    Min. Size     |   Typical Size    |
| :------------: | :--------------: | :--------------: | :---------------: |
|    Boolean     |      `bool`      |      1 byte      |      1 byte       |
|   Character    |      `char`      | 1 byte (exactly) |      1 byte       |
|                |    `wchar_t`     |      1 byte      |   2 or 4 bytes    |
|                |    `char8_t`     |      1 byte      |      1 byte       |
|                |    `char16_t`    |     2 bytes      |      2 bytes      |
|                |    `char32_t`    |     4 bytes      |      4 bytes      |
|    Integral    |     `short`      |     2 bytes      |      2 bytes      |
|                |      `int`       |     2 bytes      |      4 bytes      |
|                |      `long`      |     4 bytes      |   4 or 8 bytes    |
|                |   `long long`    |     8 bytes      |      8 bytes      |
| Floating Point |     `float`      |     4 bytes      |      4 bytes      |
|                |     `double`     |     8 bytes      |      8 bytes      |
|                |  `long double`   |     8 bytes      | 8,12, or 16 bytes |
|    Pointer     | `std::nullptr_t` |     4 bytes      |   4 or 8 bytes    |

--- end-multi-column
### 🔹 `sizeof` operator
In order to determine the size of a particular data type, C++ provides an operator named `sizeof`. The **size operator** is a *unary* operator that takes either a variable or type, and returns the size of an object of that type (in bytes). Compile and run this code as an example.

```cpp title:sizeof
#include <iostream>
#include <climits> // for char_bit

int main() {
	std::cout << "Sizeof Information:" << std::endl;
	std::cout << "===============================" << std::endl;

	std::cout << "char: " << sizeof(char) << " bytes." << std::endl;
	std::cout << "int: " << sizeof(int) << " bytes." << std::endl;
	std::cout << "unsigned int: " << sizeof(unsigned int) << " bytes." << std::endl;
	std::cout << "short: " << sizeof(short) << " bytes." << std::endl;
	std::cout << "long: " << sizeof(long) << " bytes." << std::endl;
	std::cout << "llong: " << sizeof(long long) << " bytes." << std::endl;
    
    std::cout << "================================" << std::endl;
    
    std::cout << "float: " << sizeof(float) << " bytes." << std::endl;
    std::cout << "double: " << sizeof(double) << " bytes." << std::endl;
    std::cout << "ldouble: " << sizeof(long double) << " bytes." << std::endl;
    
    std::cout << "================================" << std::endl;
    
    // below uses values defined the climits header
    
    std::cout << "Minimum Values:" << std::endl;
    std::cout << "char: " << CHAR_MIN << std::endl;
    std::cout << "int: " << INT_MIN << std::endl;
    std::cout << "short: " << SHRT_MIN << std::endl;
    std::cout << "long: " << LONG_MIN << std::endl;
    std::cout << "llong: " << LLONG_MIN << std::endl;
    
    std::cout << "=================================" << std::endl;
    
    std::cout << "Maximum Values" << std::endl;
    std::cout << "char: " << CHAR_MAX << std::endl;
    std::cout << "int: " << INT_MAX << std::endl;
    std::cout << "short: " << SHRT_MAX << std::endl;
    std::cout << "long: " << LONG_MAX << std::endl;
    std::cout << "llong: " << LLONG_MAX << std::endl;
    
    std::cout << "=================================" << std::endl;
    
    // Below shows how sizeof can be used with variable names.
    
    std::cout << "sizeof using variable names:" << std::endl;
    
    int age{21};
    std::cout << "age is " << sizeof(age) << " bytes." << std::endl;
    // OR
    std::cout << "age is " << sizeof age << " bytes." << std::endl;
    
    double wage{22.4};
    std::cout << "wage is " << sizeof(wage) << " bytes." << std::endl;
    //OR
    std::cout << "wage is " << sizeof wage << " bytes.";
	return 0;
}
```

---
### 🧠 Flashcards

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

What is the minimum size and typical size for `std::nullptr_t`?  
?|?  
Minimum size is 4 bytes — Typical size is 4 or 8 bytes.

#flashcards 