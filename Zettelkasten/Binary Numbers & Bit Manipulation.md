 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚11:12 am  📆 Sun Sep 7
 🔗 **Related Concepts**: #note #cpp
___
## 📝 Note: Binary Numbers & Bit Manipulation
When you interact with a computer—watching videos, sending messages, playing games—everything you see or hear is the result of processing electrical signals. But if you were to look inside the machine, you wouldn't find pictures or sounds stored as-is. Instead, everything is reduced to a common foundation: the **bit**, or **binary digit**.

A **bit** is the smallest unit of data in computing. At the physical level, it's implemented as a tiny switch (a transistor) that can exist in one of two states: **on** or **off**, typically represented as `1` and `0`. This binary system is not arbitrary. Digital electronics use binary because it's the most stable and reliable way to represent state. Voltage is either present (`1`) or not (`0`). There's no ambiguity, which makes binary ideal for durable computation, storage, and transmission.

But how do you represent more than just “on” or “off”?  
___
### 🔹 Binary Numbers
By combining multiple bits together, we can represent larger sets of values using **base-2 positional notation**. Just like the decimal system uses powers of 10, binary uses powers of 2.

First, consider the decimal system. In decimal, the number `4023` has:
- a `3` in the **ones** place,
- a `2` in the **tens** place,
- a `0` in the **hundreds** place,
- and a `4` in the **thousands** place.

That means we can express the number as:  
`(4 × 1000) + (0 × 100) + (2 × 10) + (3 × 1) = 4023`

Because there are 10 possible digits, each position increases by a factor of 10. This is called **base 10**.

Binary works the same way, except there are only two digits: `0` and `1`.  
This means each position increases by a factor of 2. This is **base 2**.

So, for the binary number `1101`, we calculate:  
`(1 × 8) + (1 × 4) + (0 × 2) + (1 × 1) = 13`

Add another bit to the left, and you’re now at the **16s place**. Add another, and you’re at the **32s place**, and so on.

|    Binary    | 0001  | 0010  |     0011     | 0100  |     0101      |     0110      |         0111          | 1000  |
| :----------: | :---: | :---: | :----------: | :---: | :-----------: | :-----------: | :-------------------: | :---: |
|   Decimal    |   1   |   2   |      3       |   4   |       5       |       6       |           7           |   8   |
| Place Values |   1   |   2   |    2 + 1     |   4   |      4+1      |     4 + 2     |       4 + 2 + 1       |   8   |
| Explanation  | 1 x 1 | 1 x 2 | 1 x 2 + 1 x1 | 1 x 4 | 1 x 4 + 1 x 1 | 1 x 4 + 1 x 2 | 1 x 4 + 1 x 2 + 1 x 1 | 1 x 8 |
___
--- start-multi-column: ID_5dh9
```column-settings
Number of Columns: 
Largest Column: Left
Column Spacing: 3px
Border: off
```
### 🔹 Bit Width and Value Capacity
A single bit can represent 2 possible values: `0` or `1`.

If we combine two bits, we get 4 possible combinations:
`00`, `01`, `10`, `11`

Three bits gives 8 combinations:
`000`, `001`, ..., `111`

In general, the number of possible values that can be represented with `n` bits is:


--- column-break ---

**2ⁿ**

| Bits | Possible Values |  Range (Unsigned)  |
| :--: | :-------------: | :----------------: |
|  1   |        2        |       0 to 1       |
|  2   |        4        |       0 to 3       |
|  3   |        8        |       0 to 7       |
|  4   |       16        |      0 to 15       |
|  8   |       256       |      0 to 255      |
|  16  |     65,536      |    0 to 65,535     |
|  32  |  4,294,967,296  | 0 to 4,294,967,295 |

These ranges assume **unsigned** binary numbers — meaning all values are non-negative. We'll explore signed numbers, and how negative values are represented, later using a method called **two’s complement**.

--- end-multi-column

---
### 📌 Key Definitions










---
### 🧠 Flashcards

