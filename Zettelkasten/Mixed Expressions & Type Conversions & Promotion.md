♻️ (*MinGW, Windows11, Codelite*)   
 ⌚12:31 am  📆 Thu Jul 24
 🔗 **Related Concepts**: #note #cpp [[Fundamental Data Types]], [[Operators - Basics]], [[Type Casting]]
___
##  📝 Note: Mixed Expressions & Type Conversions & Promotion
An expression involving **two or more different data types**, such as `int` and `double`.
**Example:**

- C++ operations occur on same type operands
- If operands are of different types, C++ will convert one
- Important: automatic conversion can change the result of an expression (especially with `floats` and `ints` mixed together).
- C++ will attempt to automatically convert types (coercion). If it can't, a compiler error will occur.
###  🔹 Type Conversions 
 What is it?
- Type conversion means **changing a value from one type to another.**
- This happens all the time in C++ when you're doing math with different kinds of numbers.
### 🔹 Higher vs Lower Types
Higher vs. Lower Types are based on the size of the values the **type** can hold. When C++ has to choose, it will **convert lower types to higher ones** to keep things safe.

- `double` is **higher** than `int` (it can store decimals and bigger numbers)
- `int` is **higher** than `char` (it holds bigger numbers)
- `unsigned int` and `signed int` are both 32-bit types (on most systems), but they store different values ranges, and mixing them can cause UB.

```cpp 
int a {5};
double b {2.0};
auto result = a + b; //result is promoted to double
```
- `int` (`a`) is the lower type
- `double` (`b`) is the higher type
- C++ *converts* `a` into a `double` automatically (**coercion**) so they match.

---
###  🔹 Type Coercion 
As stated above, **Type Coercion** just means that C++ automatically (at compile time) converts one type into another without you doing anything.

####  Widening Conversion **(Promotion)**
Promotion is when a type conversion/coercion moves from a smaller type to a larger type, i.e., `int -> double`, `char -> int`, etc. 
- Bit size (e.g., `int` ➡️ `long`)
- Range of values (e.g., `int` ➡️ `float`)
- Precision (e.g., `float` ➡️ `double`)
##### Example:
```cpp
short s = 42;
int i = s; // short ---> int = widening ✅
```
#####  Why it's **safe**??
- Every `short` fits inside an `int`
- No info lost
- Compiler doesn't warn you
####  Narrowing Conversion **(Demotion)**
Demotion is when conversion/coercion moves from a larger to smaller type, i.e., `double -> int` (*may* lose data!)
- Inherent risk the destination type can't hold the value
- you could lose:
	- **Range** (value to large or to small)
	- **Precision** (decimal parts get truncated)
	- **Sign** information (negatives become huge positive numbers if cast to unsigned)
##### Example:
```cpp
double d = 3.14159;
float  f = d;      // double ➡️ float = narrowing (loss of precision)
int    x = 50000;
short  y = x;      // int ➡️ short = narrowing (possible overflow)
```
#####  Why it's **unsafe**??
- You might get wrong or surprising values
- Compiler often warns (especially in modern C++)
###  🔹Numeric Ranges Cheat Sheet
|Type|Typical Bits|Range (signed)|
|---|---|---|
|`char`|8|-128 to 127|
|`short`|16|-32,768 to 32,767|
|`int`|32|±2 billion|
|`float`|32|±3.4e38 (but ~6-7 digit prec)|
|`double`|64|±1.7e308 (~15-16 digits prec)|
### 🔹 What You Actually Need to Know (Early On)
#####  The  "Integer Ladder"
```cpp
bool >> char/short >> int >> long >> long long
```
- Left to Right is "up the ladder" - Promotion"
- Right to Left is "down the ladder" - "Demotion"
>ℹ️ All values smaller than `int` are **promoted to `int`** in most arithmetic expressions, even `char`, `short`, and `bool`.
#####  The "Floating Ladder"
```cpp
float >> double >> long double
```
- ✅ Moving *up* is safe
- ⚠️ Moving *down* loses precision
#####  Signed vs. Unsigned 
```cpp
unsigned int u {10};
int i {-1};

if (i < u) {...} // i gets converted to unsigned!
```
- Signed + unsigned mixed together - unsigned wins.
- if `i` is negative, it gets turned into a *huge* positive number
###  🔹Types Hierarchy
Diagram for visual aid on types hierarchy for promotion and demotion here:
[[Types Hierarchy]]

---
###  Type Casting
Continued: 
[[Type Casting]]
