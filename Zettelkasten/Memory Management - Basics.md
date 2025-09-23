 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚11:35 pm  📆 Tue Aug 26
 🔗 **Related Concepts**: #note #cpp [[Sizeof Operator]] , [[Fundamental Data Types]]
___
## 📝 Note: Memory Management - Basics
--- start-multi-column: ID_1mjs
```column-settings
Number of Columns: 3
Largest Column: Center
Column Spacing: 3px
Border: off
```
### 🔹 Bits, Bytes, and Memory
The smallest unit of memory is the **bit** (*binary digit*), which can either be a `1` or a `0`. And while the CPU manipulates bits, the smallest **addressable** unit of memory is a **byte** (8 bits).

```text
1 bit = 1 or 0
1 byte = 2^8 combinations of 1's and 0's
```

--- column-break ---
### 🔹 Addressable Memory
A **memory address** is not a chunk of memory itself, but rather a label that tells the CPU where a particular chunk of memory is located. Each memory address corresponds to exactly 1 byte of memory, no more, no less.

```text
┌────────────┬────────────┬────────────┐
│ Address 0  │ Address 1  │ Address 2  │
│ 00000001   │ 00000010   │ 00000011   │
└────────────┴────────────┴────────────┘

```
> The CPU *sees* memory as long, contiguous row of 1-byte boxes, each with its own number (address).

--- column-break ---
### 🔹 Types in Memory
The *size* of the address depends on the CPU architecture; for example, a 64-bit CPU uses 64-bit (8 byte) memory addresses. This means the CPU can represent those addresses  with 64-bit numbers (typically represented in hexadecimal format). But no matter how wide, it still refers to a single, 1-byte chunk in memory.

```text
64-bit memory addresses
...
0x00000002
0x00000001
0x00000000
```


--- end-multi-column
___
___
___
### 🔹 How Floats Store Decimal Numbers
--- start-multi-column: ID_2irr
```column-settings
Number of Columns: 3
Largest Column: Standard
Column Spacing: 3px
Border: off
```
#### Floats use **binary scientific notation**
A number like `5.5` is stored as:

```
1.011 × 2^2
```

**This breaks into**:
- **Sign bit** (0 = positive, 1 = negative)
- **Exponent bits** (shift amount, using a bias)
- **Fraction bits** (the digits after the binary point)

--- column-break ---
#### Binary fractions use powers of 1/2:
```
0.1 = 1/2  
0.01 = 1/4  
0.001 = 1/8  
... etc
```

Only numbers made from **clean sums of those** can be stored exactly.

--- column-break ---
#### Most decimals **can’t** be stored exactly in binary
Numbers like:
- `0.1`
- `0.2`    
- `0.3`
- `0.7`
...become infinite binary fractions and get **rounded** when stored.

That’s why:
```cpp
0.1f + 0.2f != 0.3f
```

--- end-multi-column
⬇️**cont'd**⬇️
--- start-multi-column: ID_ns9e
```column-settings
Number of Columns: 3
Largest Column: standard
Column Spacing: 3px
Border: off
```
#### A float has 3 parts (32 bits total):

|  Field   |  Size   |             Purpose              |
| :------: | :-----: | :------------------------------: |
|   sign   |  1 bit  |       Positive or Negative       |
| Exponent | 8 bits  | Tells how far to shift with bias |
| Fraction | 23 bits |       Holds the precision        |

--- column-break ---
#### The Exponent Uses a Bias
- `float` uses **127** as the bias

- So:
    - Actual exponent = 2  
    - Stored = 2 + 127 = 129 → `10000001`

This lets the computer store both positive and negative exponents using only **positive** bit values.

--- column-break ---
#### Rule of Thumb:
> A decimal can be stored **exactly** in binary if it’s a fraction whose denominator is a power of 2.

Examples:
- ✅ 0.5 = 1/2
- ✅ 0.625 = 5/8
- ❌ 0.1 = 1/10
- ❌ 0.3 = 3/10

--- end-multi-column

___
___
___
### 🔹 Storing values and memory
Consider the following:

```cpp
int x{5};
// vs.
int x = 5;
```

> **Both of the initializations tell the compiler this**:
> 
> *Give me a piece of memory of the size of type*,  `int` *and store value* `5` *in there. Also, allow me to refer to that memory location as* `x`.

Both end up creating the same memory layout in most cases:
- A memory block is allocated (usually 4-bytes for `int`).
- The value `5` is **written** into that block of memory.
- The name `x` is bound to that memory location (because `x` refers to location in memory, not the value).

However, the syntax of how you initialize objects changes the rules for how the compiler checks and converts the value you are trying to store. See [[Assignment & Initialization]] for more details.
___
___
___
### 🔹 Dynamic Memory Allocation
TBD
___
___
___





---
### 📌 Key Definitions










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

