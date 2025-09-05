 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚9:58 pm  📆 Wed Sep 3
 🔗 **Related Concepts**: #note #cpp [[Sizeof Operator]] , [[Pointers and References]] , [[Memory Management - Basics]]
___
## 📝 Note: Fundamental Data Types
### 🔹 Bits, Bytes, and Memory
The smallest unit of memory is the **bit** (*binary digit*), which can either be a `1` or a `0`. And while the CPU manipulates bits, the smallest **addressable** unit of memory is a **byte** (8 bits).

```text
1 bit = 1 or 0
1 byte = 2^8 combinations of 1's and 0's
```
### 🔹 Addressable Memory
A **memory address** is not a chunk of memory itself, but rather a label that tells the CPU where a particular chunk of memory is located. Each memory address corresponds to exactly 1 byte of memory, no more, no less.

```text
┌────────────┬────────────┬────────────┐
│ Address 0  │ Address 1  │ Address 2  │
│ 00000001   │ 00000010   │ 00000011   │
└────────────┴────────────┴────────────┘

```
> The CPU *sees* memory as long, contiguous row of 1-byte boxes, each with its own number (address).

### 🔹 Types in Memory
The *size* of the address depends on the CPU architecture; for example, a 64-bit CPU uses 64-bit (8 byte) memory addresses. This means the CPU can represent those addresses  with 64-bit numbers (typically represented in hexadecimal format). But no matter how wide, it still refers to a single, 1-byte chunk in memory.

```text
64-bit memory addresses
...
0x00000002
0x00000001
0x00000000
```
### 🔹 Data Types
A **Data Type** or just *type* defines the kind of value an object can store, such as an `int`, `char`, `float`, etc. It's important because the type tells the compiler how to interpret and store that value in memory so it can be correctly translated into binary data. **Fundamental Data Types**—informally referred to as *primitive* data types—come predefined in the C++ language and are available for us to use without the STL. 
### 🔹Fundamental Data Types
Fundamental Data types can be generally categorized as such:
--- start-multi-column: ID_cq1c
```column-settings
Number of Columns: 3
Largest Column: Left
Column Spacing: 3px
Border: off
```
##### Floating Point Types
- `float`
- `double`
- `long double`

These values are represented as fractional digits, either negative or positive, i.e., `-2.0`, `-1.5`, `-0.555`, `0.0`, `3.14159`, etc.

--- column-break ---
##### Null Pointer
- `std::nullptr_t` (C++ 11)

We will refer to `nullptr` in [[Pointers and References]]

--- column-break ---
##### Void
- `void`
No type

--- end-multi-column
________
--- start-multi-column: ID_d7us
```column-settings
Number of Columns: 3
Largest Column: center
Column Spacing: 3px
Border: off
```
##### Integral Type: **Boolean**
	- `bool`

A bool stores a truth value: either `true` or `false`.

--- column-break ---
##### Integral Type: **Character**
	- `char`
	- `wchar_t`
	- `char8_t` (C++ 20)
	- `char16_t` (C++ 11)
	- `char32_t` (C++ 11)

These values represent single characters of text (letters, numeric characters, and symbols) . 'a', 'A', '?', '4' etc.

--- column-break ---
##### Integral Type: **Integer**
	- `int`
	- `short int`
	- `long int`
	- `long long int` (C++ 11)

These values represent whole numbers, positive, negative and 0.

--- end-multi-column
### 🔹 Integer vs. Integral Types
In mathematics, an **integer** is a whole number, no decimal or fractional part, and it can be positive, negative or zero. The term "integral" in the context of C++ means "*Like an integer*". 

> 💡 Integral types only refer to fundamental data types. **Enums** and **Enum Classes** are not integral types.
#### Nomenclature
The term "Built-in" data type is used synonymously when referring to fundamental, or primitive data types. Generally, it is best to avoid this term because the creator of C++ and other contributors define compound data types and fundamental data types as *built-in*. With that being said there are two other categories of data types we will cover later. [[Compound Data Types]] and [[Standard Library(STUB)|Standard Library Types]].
### 🔹 The `_t` suffix
The `_t` suffix literally stands for **type**, and it appears in often in modern C++ to signal that a given identifier is a type alias. When you see this suffix, it usually means:
- It's an **alias** to a more complex type.
- It's intended to be used like a regular type, not as a variable or function.
- It often conveys precision or purpose (e.g., `int8_t` vs `char`)
---
### 🧠 Flashcards

What is the smallest unit of memory the CPU can directly manipulate?  
?|?  
A **bit** (binary digit), which can be either `0` or `1`.

---

What is the smallest **addressable** unit of memory on modern CPUs?  
?|?  
A **byte**, which is 8 bits.

---

What does a memory address represent?  
?|?  
A **label** used by the CPU to identify the location of a single byte of memory.

---

Does increasing the address width (e.g., from 32-bit to 64-bit) increase the size of a memory address?  
?|?  
Yes — a 64-bit architecture uses **8-byte wide** addresses, allowing more total memory to be addressed.

---

What does a **data type** define in C++?  
?|?  
It defines the **kind of value** an object can store and tells the compiler how to **store and interpret** the value in memory.

---

What are **fundamental** (or **primitive**) data types in C++?  
?|?  
They are the **built-in** types provided by the language, like `int`, `char`, `float`, `bool`, and `void`.

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

#flashcards 