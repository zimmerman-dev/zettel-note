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

