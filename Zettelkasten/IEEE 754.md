 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚9:54 pm  📆 Tue Sep 9
 🔗 **Related Concepts**: #note #cpp
___
## IEEE-754 Floating Point — A Gentle Introduction

### Pre-requisite
Before we talk about floating point, let’s remind ourselves of a few pre-requisite topics. Firstly, converting **decimal to binary** and then we can look at **scientific notation**.

### 0. Converting Decimal to Binary

To read floating point numbers, we need to know how to write numbers in **binary (base 2)**.

-   Whole numbers are divided by 2 repeatedly, tracking remainders.  
-   Fractions are multiplied by 2 repeatedly, tracking integer parts.
    
#### Note on Subscripts
When you see something like $13_{10}$, the subscript tells you the base:

-   $13_{10}$ means "13 in base 10" (decimal).    
-   $1101_{2}$ means "1101 in base 2" (binary), which equals 13 in decimal.
    
#### Example 1: Whole Number
Convert $13_{10}$ to binary:

-   $13 \div 2 = 6$ remainder $1$  
-   $6 \div 2 = 3$ remainder $0$    
-   $3 \div 2 = 1$ remainder $1$    
-   $1 \div 2 = 0$ remainder $1$  

> Reading remainders bottom to top: $13_{10} = 1101_2$.
    
#### Example 2: Fraction
Convert $0.625_{10}$ to binary:

-   $0.625 \times 2 = 1.25$ → take $1$    
-   $0.25 \times 2 = 0.5$ → take $0$    
-   $0.5 \times 2 = 1.0$ → take $1$  
  
So $0.625_{10} = 0.101_2$.
    
#### Putting It Together
$13.625_{10} = 1101.101_2$

----------

### 1. Scientific Notation Refresher (Decimal → Binary)

In decimal (base 10):  
$5600 = 5.6 \times 10^3$  

We moved the decimal point three places left, and recorded that movement as $10^3$.

In binary (base 2), the idea is the same.  
$101.1_2 = 1.011 \times 2^2$  

Here, we shifted the binary point two steps left and tracked it with $2^2$.  
This trick—“one digit before the point, then a power for the shifts”—is exactly what floating point uses.

----------

### 2. Why We Need a Rulebook

Computers don’t store decimals like humans do. They only store 1s and 0s. But many decimals (like $0.1$) can’t be written exactly in binary.

Example:  
$0.1_{10} = 0.0001100110011\ldots_2$  

It repeats forever.

If each computer chopped that repeating fraction differently, then $0.1 + 0.2$ could give slightly different results on every machine. One might say $0.3000001$, another $0.2999999$.

To avoid chaos, everyone agreed on a standard: **IEEE-754**. It tells computers exactly how to break numbers into parts, how to round them, and how to agree on results.

----------

### 3. Breaking Numbers Into Pieces

IEEE-754 splits every floating-point number into three parts:

1.  **The sign bit** → Are we positive or negative?   
2.  **The exponent** → How far the binary point jumps.    
3.  **The mantissa (fraction field)** → The detailed digits after the binary point.
    
For a 32-bit float, the layout is:

| Sign (1 bit) | Exponent (8 bits) |   Mantissa (23 bits)    |
|--------------|-------------------|-------------------------|
| 0            | 10000001          | 01100000000000000000000 |
|

_(Example above is for 5.5)_

#### Example: 6.25

1.  Write $6.25$ in binary:  
    $6.25_{10} = 110.01_2$
    
2.  Normalize it:  
    $110.01_2 = 1.1001 \times 2^2$
    
3.  Break it down:
    
    -   Sign = $0$ (positive).        
    -   Exponent = $2$ (we shifted 2 places).       
    -   Mantissa = $1001$ (the part after the point).
        
So $6.25$ would be stored as:  

$\text{Sign} = 0, \quad \text{Exponent} = 2 + \text{bias}, \quad \text{Mantissa} = 1001\ldots$  

We’ll see the bias trick in a moment.

----------

### 4. The Magic Formula

Every IEEE-754 floating point number follows this formula:  

$(-1)^{\text{sign}} \times 2^{(\text{stored exponent} - \text{bias})} \times (1 + \text{mantissa})$

-   The $(-1)^{\text{sign}}$ makes the number positive or negative.
-   The exponent in the bits isn’t the real exponent—it’s “biased.”    
-   The mantissa is the fractional detail after the binary point.
    
#### About the Bias
The bias is just a fixed offset to avoid negative numbers in the exponent field.

-   For 32-bit floats, bias = $127$.    
-   For 64-bit doubles, bias = $1023$.
    
**Encoding:**  
$\text{Stored exponent} = \text{Real exponent} + \text{Bias}$

**Decoding (using the formula):**  
$\text{Real exponent} = \text{Stored exponent} - \text{Bias}$

Example with $6.25$:

-   Real exponent = $2$.    
-   Stored exponent = $2 + 127 = 129$.    
-   When decoding: $129 - 127 = 2$.
    
----------
### 5. Anatomy of a Float (32-bit)
A float is 32 bits split as:


| 1 bit sign | 8 bits exponent | 23 bits mantissa |
|------------|-----------------|------------------|
|

Bias = 127.
#### Example: 5.5
1.  Binary form:  
    $5.5_{10} = 101.1_2$
    
2.  Normalize:  
    $101.1_2 = 1.011 \times 2^2$
    
3.  Fields:
    -   Sign = $0$.      
    -   Stored exponent = $2 + 127 = 129 \to 10000001_2$.     
    -   Mantissa = $011$.
        
Final layout:

```
0 10000001 01100000000000000000000

```

----------
### 6. Double Precision (64-bit)

Same pattern, but with more bits:


| 1 bit sign | 11 bits exponent | 52 bits mantissa |
|------------|------------------|------------------|
|

Bias = $1023$.  

This gives more precision and a wider range of values.

----------
### 7. Special Rules
Not every pattern of bits maps to a normal number. IEEE-754 defines special cases:

-   Exponent = all 0s → subnormal numbers (tiny values, no hidden 1).
-   Exponent = all 1s → infinity or NaN (“Not a Number”).    
-   Mantissa = 0 → exact powers of two.
    
----------
### 8. Limits and Rounding
Floats have limited mantissa bits:

-   23 bits for float.    
-   52 bits for double.
    
That means fractions like $0.1$ or $\tfrac{1}{3}$ don’t fit exactly. They get rounded to the nearest representable number.

Example in C++:

```cpp
std::cout << 0.1;
// 0.10000000149011612
```

That’s not wrong—it’s just the closest binary approximation.

----------
### 9. Big Picture

Floating point is just **scientific notation in base 2**.

-   Sign bit = the plus/minus switch.    
-   Exponent = how far the decimal point hops.    
-   Mantissa = the zoomed-in detail.    
-   Limits = like building with a fixed number of Lego bricks—you can’t always make the perfect shape, only the closest one.

----------
### 10. Where This Connects
-   [[Floating-Point Types]]   
-   [[Binary Numbers - Basic]] 
-   [[Memory Management - Basics]] 

    





























___
### 📌 Key Definitions










___
### 🧠 Flashcards

