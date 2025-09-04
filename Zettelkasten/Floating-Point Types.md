♻️ (*MinGW, Windows11, Codelite*)   
 ⌚10:00 pm  📆 Thu Aug 14
 🔗 **Related Concepts**: #note #cpp [[Data Types]], [[Mixed Expressions & Type Conversions & Promotion]]
___
##  What are Floating-point Numbers?
A variable declared to be of type **float** can be used for storing values containing decimal places. To simplify, a **floating point number** represents a real number i.e., numbers that can have decimals, like `3.14`, `-0.00001`, or `2.4545`.

- They are useful for measuring things that aren't whole: Time, weight, temperature, velocity, etc.
- **Think of them like scientific notation in binary**. A number + a fractional part + an exponent.
### 📌 `float num = 3.14` vs. `float num = 3.14f`
### 🔹 Main Floating-Point Types in C++

| Type          | Size (Typical) | Precision (Decimal Digits)        | Use Case                           |
| ------------- | -------------- | --------------------------------- | ---------------------------------- |
| `float`       | `4 bytes`      | `~6-7 digits`                     | Lightweight math, graphics         |
| `double`      | `8 bytes`      | `~15-16 digits`                   | General use (default literal type) |
| `long double` | `8-16 bytes`   | at least `double`, sometimes more | Rarely needed                      |
>Depends on compiler/platform. On many systems, `long double` is the same as `double`.
---
### 🔹 Key Concept: Precision *is not* Accuracy
- **Precision** = how many digits you *choose* to display (or store)
- **Accuracy** = how close the value is to the *true mathematical result*
- **Example**: `0.1` **cannot be stored exactly in binary** — this is why floating-point math can result in subtle rounding errors
```cpp
#include <iostream>
#include <iomanip>

int main() {
    float sum {1.0f / 3.0f};
    
    std::cout << std::setprecision(10);
    std::cout << sum << '\n'; // Output: 0.3333334333
}                             
```
> 🔍 Computers use **base 2**, not base 10 — so many decimals like `0.1`, `0.3`, `1/3`, etc., **can’t be represented precisely**. The weird decimal behavior is from binary approximation, _not bad math_.

👇 For readability and output safety, use `std::fixed` with `std::setprecision()` when displaying floats.
___
### 🔹 `std::setprecision()`, `std::fixed`, & scientific notation (see: <iomanip\>)
- `std::setprecision(n)` sets the **number of significant digits** — _unless used with `std::fixed`, then it sets digits after the decimal_.
- It acts like a **stream manipulator** (not a function you call). 
```cpp
std::cout << std::setprecision(4);
// All following float/double output is affected
```
####  Behavior Table (*without* `std::fixed`)
```cpp 
std::cout << std::setprecision(4);
// 0.000444444 ---> 0.0004444 ---> Leading zeros after decimal don't count as significant digits
// 0.00045678  ---> 0.0004568 ---> Rounds the 4th digit up, based on next (7)
// 0.11011111  ---> 0.1101    ---> 4 sig digits: 1,1,0,1; rounds, then stops
// 9.9999      ---> 10.00     ---> Rounds across decimal, triggers cascading carry-up
```
### 🔹 How does `std::fixed` behave?
On its own, `std::fixed` doesn't do much. `std::cout` shows 6 significant digits by default, so `std::fixed` by itself outputs the default 6 decimal places, padded with zeros. What makes it interesting is when you combine it  with `std::setprecision(n)`.  Let’s break down what happens when `std::fixed` meets `std::setprecision()`.

By default, `std::setprecision(n)` controls the total number of significant digits. But once you add `std::fixed`, it switches to controlling the number of digits **after the decimal point**, regardless of the number’s magnitude.
```cpp
std::cout << std::fixed << std::precision(n);
// all following float/double output is affected
```
####  Behavior Table (*with* `std::fixed`)
```cpp 
std::cout << std::fixed << std::setprecision(4);
// 3.14159265359 ---> 3.1416 ---> Digits after decimal are clipped at 4 and the 5 is rounded to 6 due to the 9.
// 1.1           ---> 1.1000 ---> Digits after the 1 are filled in with 0s
// 1.99999       ---> 2.0000 ---> Digits are rounded to 2
// 1.9           ---> 1.9000 ---> No rounding — padding occurs to match 4 digits after decimal.
```
### 🔹 TL;DR:  
Use `std::setprecision(n)` when you care about **how much to show**,  
Use `std::fixed` when you care about **how it looks**.
When using scientific notation, `e` replaced `10^`.
___
### 🔹 `f` Literal Suffix
```cpp
float x = 3.14f;
```
 - `f` tells the compiler to treat the number as a `float` (not `double`)
- Without it, `3.14` is a `double` by default
- Helps avoid _narrowing conversions_ or unwanted precision
> 💡 Rule of thumb: Use `f` when assigning to `float` variables
___
### 🔹 2. Scientific Notation
While you can write floats normally, it's also viable to write digits in scientific notation.  For example, `1.2 x 10^4` would be written as `1.2e4`, and `5.9722 x 10^24` would be written as `5.9722e24`.
___
### 🔹 Why Floating-Path Math Can Be Weird
- Computers use **binary fractions**.
- *Just like how `1/3` is **hard to express** in `base 10`, `0.1` is **hard to express** in `base 2`.*
- **Direct comparisons like `a == b` can fail** — even if both values look the same when printed. 
	- Example: Adding `0.1 + 0.2` might not exactly equal `0.3` in memory.
