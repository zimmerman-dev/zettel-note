 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚9:42 pm  📆 Thu Sep 18
 🔗 **Related Concepts**: #note #cpp [[Binary Numbers - Basic]] , [[IEEE 754]] , [[Arithmetic Conversions(STUB)]]
___
## 📝 Note: Numeral Systems
Most of the stuff on binary will be covered in [[Binary Numbers - Basic]] and [[IEEE 754]]. With that in mind this note will be the place I compile all my notes on **hexadecimal** and **octal** unless I find it necessary later to expand those concepts into their own notes. 

--- start-multi-column: ID_u6cw
```column-settings
Number of Columns: 3
Largest Column: Standard
Column Spacing: 3px
Border: off
```
### 🔹 Binary (Base-2)
- Uses only `0` and `1`
- Each position is a power of **2**
- Rightmost bit = `2^0`, next = `2^1`, etc.
- `0b` is the pre-fix for binary
####  Mental Model:
- Each bit is a **light switch** — on (`1`) or off (`0`) — powering a different `2^n` circuit
####  Example:
```txt
Binary: 1011
= (1*8) + (0*4) + (1*2) + (1*1)
= 11 (decimal)
```

--- column-break ---
### 🔹 Decimal (Base-10)
- Uses `0` to `9`
- Each digit's place is a power of **10**
- Familiar system used in everyday math
#### Example:
```txt
Number: 425
= 4×100 + 2×10 + 5×1
= 400 + 20 + 5 = 425
```

--- column-break ---
### 🔹 Hexadecimal (Base-16)
- Uses `0`–`9` and `A`–`F`
- `A` = 10, `B` = 11, ..., `F` = 15
- Each digit’s place is a power of **16**
- `0x` is the literal pre-fix for hex
####  Mental Model:
- Each **hex digit = 4 binary bits**  
- Hex is just a **shorthand for binary**
####  Example:
```txt
Hex: 0xB4
= B×16^1 + 4×16^0
= 11×16 + 4 = 176 + 4 = 180 (decimal)
```

--- end-multi-column
##  Conversions
--- start-multi-column: ID_44aw
```column-settings
Number of Columns: 3
Largest Column: Standard
Column Spacing: 3px
Border: off
```
#### Binary ↔ Hex
- Group binary into **4-bit chunks (nibbles)** from right to left
- Each nibble becomes one hex digit
#### Example:
```txt
Binary: 10110100  
→ 1011 0100  
→ B 4  
→ Hex: 0xB4
```

--- column-break ---
#### Binary ↔ Decimal
- Multiply each bit by its corresponding `2^position`
- No nibble grouping allowed — all place values must be used
#### Example:
```txt
Binary: 11101000  
= 1×128 + 1×64 + 1×32 + 0×16 + 1×8 + 0×4 + 0×2 + 0×1  
= 232 (decimal)
```

--- column-break ---
#### Hex ↔ Decimal
- Multiply each digit by its `16^position`, starting from right
#### Example:
```txt
Hex: 0x2A  
= 2×16^1 + 10×16^0  
= 32 + 10 = 42
```

--- end-multi-column
___
### 📌 Summary Tips
- **Hex → Binary**: One hex digit = one 4-bit group
- **Binary → Decimal**: Use full powers of 2 (no shortcuts)
- **Hex → Decimal**: Multiply each digit by 16^position
- **Decimal → Hex**: Divide by 16 repeatedly, track remainders
- Use **Hex** as a visual shorthand for binary in low-level code (memory addresses, flags, bit masks)
___
### 🧠 Flashcards

What is the binary equivalent of the hex digit D?
?|?
1101

___

Convert binary 10011100 to hexadecimal.
?|?
0x9C

___

What does each hex digit represent in terms of bits?
?|?
4 bits (1 nibble)

___

Convert hex 0xA7 to binary.
?|?
10100111

___

What is the decimal value of binary 11001010?
?|?
202

___

Describe the conversion process from binary to decimal.
?|?
Multiply each bit by 2^position (starting from the right), then sum.

___

What is the decimal value of 0x1F?
?|?
31

___

Convert 0x2D to decimal.
?|?
45

___

How do you convert a hexadecimal number to decimal?
?|?
Multiply each digit by 16^position (right to left), then sum.

___

Why is hex used in programming instead of binary?
?|?
It's compact and readable; each digit maps cleanly to 4 binary bits.

___

What is the value of hex digit F in decimal?
?|?
15

___

What are the valid digit symbols in hexadecimal?
?|?
0–9 and A–F (case-insensitive)

___

What is the base of the decimal system?
?|?
10

___

What does "nibble" refer to in binary?
?|?
A group of 4 bits


#flashcards 