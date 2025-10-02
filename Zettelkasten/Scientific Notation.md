 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚11:25 pm  📆 Mon Sep 8
 🔗 **Related Concepts**: #note #cpp [[Fundamental Data Types]] , [[Binary Numbers - Overview]]
___
## 📝 Note: Scientific Notation
This note is an intro to scientific notation, and should be considered a pre-requisite read before moving on to [[Floating-Point Types]]. **Scientific Notation** is a useful shorthand for writing large or small numbers in a standardized and concise way.  Gaining a firm grasp on it will prepare you for understanding how floating-point numbers work, and more importantly, what their **limitations** are.
### 🔹 Formula
Numbers in scientific notation take the following form:  
$significand \times 10^x$  

For example:
$1.2 \times 10^4 = 12,\!000$

- Significand = $1.2$  
- Exponent = $4$

This would be represented as $1.2e4$

> ✅ By convention, the significand is always written with **one digit before the decimal**, and the rest after.  The exponent indicates how many places the decimal point has been shifted to represent the original number.
___
#### 🌍 Example: Mass of the Earth
- In decimal notation:
5,972,200,000,000,000,000,000,000

In scientific notation:
- Significand = $5.9722$
- Exponent = $10^{24}$  
- Final expression: $5.9722  10^{24}$
### 🔹 Converting decimal numbers to scientific notation
#### Step 1: **Identify the first non-zero digit**
This will be the **start of your significand**.
#### Step 2: **Place the decimal** right _after_ that first digit
This gives you the proper format:  
→ **1 digit before the decimal**, the rest after.
#### Step 3: **Count how many places** the decimal moved
This becomes your **exponent** on the base 10:
- Moved right → **negative** exponent
- Moved left → **positive** exponent
#### Step 4: **Assemble final format**
```txt
significand × 10^exponent
```
### 📌 Rules of Thumb
- Always 1 digit **before** the decimal
- Count the shift **from original decimal to new decimal**
- Use **positive exponent** for big numbers
- Use **negative exponent** for tiny numbers
- Drop trailing zeros unless precision matters