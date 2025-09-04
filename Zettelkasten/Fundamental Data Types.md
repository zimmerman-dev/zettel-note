 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚9:58 pm  📆 Wed Sep 3
 🔗 **Related Concepts**: #note #cpp [[Sizeof]] , [[Pointers and References]] , [[Memory Management - Basics]]
___
## 📝 Note: Fundamental Data Types
--- start-multi-column: ID_md9t
```column-settings
Number of Columns: 3
Largest Column: standard
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
> The CPU *see's* memory as long, contiguous row of 1-byte boxes, each with its own number (address).

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
### 🔹 Fundamental Data Types
All data on a computer is just a sequence of bits. We use a **data type** or just type to tell the compiler how to interpret the contents of memory in a meaningful way.

































---
### 📌 Key Definitions










---
### 🧠 Flashcards

