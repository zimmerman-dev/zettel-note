 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚9:54 pm  📆 Tue Sep 9
 🔗 **Related Concepts**: #note #cpp
___
## 📝 Note: IEEE 754

## **Summary: How Floats Store Decimal Numbers**

### 🔹 Floats use **binary scientific notation**

A number like `5.5` is stored as:

```
1.011 × 2^2
```

This breaks into:

- **Sign bit** (0 = positive, 1 = negative)
- **Exponent bits** (shift amount, using a bias)
- **Fraction bits** (the digits after the binary point)
---
### 🔹 Binary fractions use powers of 1/2:
```
0.1 = 1/2  
0.01 = 1/4  
0.001 = 1/8  
... etc
```

Only numbers made from **clean sums of those** can be stored exactly.
___
### 🔹 Most decimals **can’t** be stored exactly in binary
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

---

### 🔹 A float has 3 parts (32 bits total):

| Field    | Size    | Purpose                            |
| -------- | ------- | ---------------------------------- |
| Sign     | 1 bit   | Positive or negative               |
| Exponent | 8 bits  | Tells how far to shift (with bias) |
| Fraction | 23 bits | Holds the precision digits         |

---

### 🔹 The Exponent Uses a Bias

- `float` uses **127** as the bias
    
- So:
    
    - Actual exponent = 2
        
    - Stored = 2 + 127 = 129 → `10000001`
        

This lets the computer store both positive and negative exponents using only **positive** bit values.

---

### 🔹 Rule of Thumb:

> A decimal can be stored **exactly** in binary if it’s a fraction whose denominator is a power of 2.

Examples:

- ✅ 0.5 = 1/2
    
- ✅ 0.625 = 5/8
    
- ❌ 0.1 = 1/10
    
- ❌ 0.3 = 3/10
    





























___
### 📌 Key Definitions










___
### 🧠 Flashcards

