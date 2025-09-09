 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚11:25 pm  📆 Mon Sep 8
 🔗 **Related Concepts**: #note #cpp [[Fundamental Data Types]] , [[Binary Numbers & Bit Manipulation]]
___
## 📝 Note: Scientific Notation
This note is an intro to scientific notation, and should be considered a pre-requisite read before moving onto [[Floating-Point Types]]. **Scientific Notation** is a useful shorthand for writing lengthy numbers in a standardized and concise way. Gaining a firm grasp on scientific notation will help prepare you for understanding how floating-point numbers work, and more importantly, what their limitations are.
### 🔹 Formula
Numbers in scientific notation take the following form: $significand * 10^{x}$. For example, consider this number represented in scientific notation: $1.2 * 10^4$.
- Significand = $1.2$
- Exponent = $10^4$
Thus, $1.2 * 10^4 = 12000$.

> By convention, numbers in scientific notation are written one digit before the decimal point, and the rest of the digits afterward. The exponent is just the amount of zeros is found by rounding down to the nearest decimal placement.
#### Example
Consider the mass of the earth. In decimal notation, we'd write this as 5,972,200,000,000,000,000,000,000. Well, with that in mind:
- Significand = $5.9722$
- Exponent = $10^{24}$
Final equation: $5.9722 * 10^{24}$.



## 📝 Note: Scientific Notation
This note is an intro to scientific notation, and should be considered a pre-requisite read before moving on to [[Floating-Point Types]]. **Scientific Notation** is a useful shorthand for writing large or small numbers in a standardized and concise way.  Gaining a firm grasp on it will prepare you for understanding how floating-point numbers work, and more importantly, what their **limitations** are.
### 🔹 Formula
Numbers in scientific notation take the following form:  
$significand \times 10^x$  

For example:
$1.2 \times 10^4 = 12,\!000$

- Significand = $1.2$  
- Exponent = $4$

> ✅ By convention, the significand is always written with **one digit before the decimal**, and the rest after.  The exponent indicates how many places the decimal point has been shifted to represent the original number.
___
#### 🌍 Example: Mass of the Earth
- In decimal notation:
5,972,200,000,000,000,000,000,000

In scientific notation:
- Significand = $5.9722$
- Exponent = $10^{24}$  
- Final expression: $5.9722  10^{24}$
### ]







































How to convert decimal numbers to scientific notation

Use the following procedure:

- Your exponent starts at zero.
- If the number has no explicit decimal point (e.g. `123`), it is implicitly on the right end (e.g. `123.`)
- Slide the decimal point left or right so there is only one non-zero digit to the left of the decimal.
    - Each place you slide the decimal point to the left increases the exponent by 1.
    - Each place you slide the decimal point to the right decreases the exponent by 1.
- Trim off any leading zeros (on the left end of the significand)
- Trim off any trailing zeros (on the right end of the significand) only if the original number had no decimal point. We’re assuming they’re not significant. If you have additional information to suggest they are significant, you can keep them.

___
### 📌 Key Definitions










___
### 🧠 Flashcards

