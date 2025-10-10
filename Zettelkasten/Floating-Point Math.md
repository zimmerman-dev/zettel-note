 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:17 am  📆 Sat Sep 27
 🔗 **Related Concepts**: #note #cpp [[Floating-Point Types]] , [[IEEE 754]] 
___
## 📝 Note: Floating-Point Math
This is a note of some of the more common floating point math hurdles one will come across.
### 🔹 Comparing Floating-Point Values with `epsilon`
When comparing floating-point values (`float`, `double`, `long double`), direct equality (`==`) is **not reliable** due to rounding errors and precision limitations. Even mathematically "equal" expressions might differ by a tiny amount in binary form.
####  Problem:
```cpp
double x{0.3}; double y{0.2 + 0.1};  
std::cout << (x == y);  // ⚠️ Might print false
```
Even though `0.2 + 0.1` is mathematically `0.3`, floating-point math introduces small rounding errors. That’s where **epsilon** comes in.
#### ✅ Solution: Use a "close enough" comparison
```cpp
#include <cmath>      // for std::abs 
#include <limits>     // for std::numeric_limits  
if (std::abs(x - y) < std::numeric_limits<double>::epsilon()) {   
// close enough: x and y are treated as equal 
}
```
### 🔹 What is `epsilon`?
- `epsilon` is the smallest possible difference between `1.0` and the next representable `double` value.   
- Think of it as a tiny buffer that accounts for floating-point imprecision.  
- Access it via `std::numeric_limits<T>::epsilon()` where `T` is your type (`float`, `double`, etc.).  
### 🔹 Custom Tolerance
For real-world comparisons, `epsilon` may be **too small**. It’s often better to use your own tolerance:

```cpp
double tolerance{1e-8}; 
if (std::abs(a - b) < tolerance) {
   // close enough for practical purposes 
}
```
### 🔹 Summary
- Never use `==` to compare floating-point numbers. 
- Use `std::abs(a - b) < epsilon` or your own small threshold.  
- This applies to `!=` as well: instead of checking for "not equal", check if the difference is _greater than_ a small tolerance.
- See: [[Operators - Relational & Logical]]



























___
### 📌 Key Definitions










___
### 🧠 Flashcards

