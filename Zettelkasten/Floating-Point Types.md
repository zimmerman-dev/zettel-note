♻️ (*MinGW, Windows11, Codelite*)   
⌚10:00 pm  📆 Thu Aug 14  
🔗 **Related Concepts**: #note #cpp [[Fundamental Data Types]], [[Mixed Expressions & Type Conversions & Promotion]]
___
## 📝 Floating-Point Types
Before getting to **floating point types**, I'd like to first define what a real number is in general mathematics. A **real number** is a number within the set of all rational and irrational numbers. **Real Numbers can be:**
- Positive, negative, or zero
- Fractional/decimal
- Irrational (e.g., $\sqrt{{2}}$, $\pi$, $e$)

--- start-multi-column: ID_tdtg
```column-settings
Number of Columns: 2
Largest Column: Right
Column Spacing: 3px
Border: off
```
### 🔹 Floating Point Numbers (C++)

In C++, **Floating Point Numbers** are *real numbers* represented in a binary floating format (IEEE-754), albeit with caveats. This means that in C++, floating point numbers can be:

- Positive, negative, or zero in decimal form: $0.0$
- Fractional decimals: $0.25$
- Scientific notation: $1.2e4$

> ⚠️ Because storage is finite, floating point numbers are **approximations** of real numbers — meaning not every number can be stored exactly (e.g., $0.\overline{{3}}$).

--- column-break ---

### 🔹 Floating Point Types (C++)

C++ provides three floating point types (`float`, `double`, and `long double`) as part of its fundamental types:

```cpp
float       // Usually 32 bits → ≈ 7 decimal places of precision
double      // Usually 64 bits → ≈ 16 decimal places of precision
long double // Usually 80+ bits → Precision varies by platform
```

- The floating point **type** determines the range and precision.
- `double` is the default type for floating point literals.

--- end-multi-column
___
### 🔹 Floating Point Type Sizes and Ranges
In floating-point representation:
- **Range** is controlled by the number of exponent bits
- **Precision** is controlled by the number of mantissa (significand) bits

|          IEEE Format          |    C++ Type    |             Approximate Range             |      Approx. Precision       |
| :---------------------------: | :------------: | :---------------------------------------: | :--------------------------: |
|   Single Precision (32-bit)   |    `float`     |   ±1.18 × 10⁻³⁸ to ±3.4 × 10³⁸ and 0.0    | ~6–9 significant digits (≈7) |
|   Double Precision (64-bit)   |    `double`    |  ±2.23 × 10⁻³⁰⁸ to ±1.80 × 10³⁰⁸ and 0.0  |     ~15–18 digits (≈16)      |
|  Extended Precision (80-bit)  | `long double`* | ±3.36 × 10⁻⁴⁹³² to ±1.18 × 10⁴⁹³² and 0.0 |        ~18–21 digits         |
| Quadruple Precision (128-bit) |  non-standard  | ±3.36 × 10⁻⁴⁹³² to ±1.18 × 10⁴⁹³² and 0.0 |        ~33–36 digits         |

📝 *Mantissa (aka significand)*: the part of a floating point number that contains its significant digits.

The 80-bit x87 extended-precision floating point type is unique. It’s usually padded to 12 or 16 bytes for alignment, but only 80 bits are used for data.

Despite similar exponent ranges between 80-bit and 128-bit types, the 128-bit format provides **greater precision** due to a larger mantissa.

See: [[IEEE 754]]
#### Guiding Principles
- `float` is typically 4 bytes (32 bits)
- `double` is typically 8 bytes (64 bits)
- `long double` varies and may not follow IEEE-754 — avoid it for portable code.

___
### 🔹 Precision
Let's return from the technical weeds for a moment:

> *Because storage is finite, floating point numbers are **approximations** of real numbers.*

A value like $0.\overline{{3}}$ would require infinite memory. A `float` (≈7 digits) or `double` (≈16 digits) can only represent a subset of possible values, leading to **loss of precision** in many real-world cases.

___
### 🔹 Outputting Floating Point Values
`std::cout` uses a default precision of **6 significant digits** — meaning it assumes you're outputting `float`s and will truncate accordingly.

```cpp
#include <iostream>

int main()
{
    std::cout << 9.87654321f << '\n';
    std::cout << 987.654321f << '\n';
    std::cout << 987654.321f << '\n';
    std::cout << 9876543.21f << '\n';
    std::cout << 0.0000987654321f << '\n';

    return 0;
}
```

___
### 🔹 `std::setprecision()`
- Sets **significant digits** unless combined with `std::fixed`, in which case it sets **decimal places**.

```cpp
#include <iostream>
#include <iomanip>

int main() {
    float sum {{1.0f / 3.0f}};
    std::cout << std::setprecision(10);
    std::cout << sum << '\n'; // 0.3333334333
}
```

> Computers use **base 2**, not base 10 — so many decimals like `0.1` or `1/3` can’t be precisely represented in binary.

---
### 🔹 `std::fixed` Behavior
When you combine `std::fixed` with `std::setprecision(n)`, you tell the stream: “show `n` digits **after the decimal point**, always.”

```cpp
std::cout << std::fixed << std::setprecision(4);
```

Example behavior:

- `3.14159265359` → `3.1416`
- `1.1`           → `1.1000`
- `1.99999`       → `2.0000`
- `1.9`           → `1.9000`

✅ Use `std::fixed` when formatting output for people. Use `std::setprecision()` alone when you care about scientific detail.

___
### 🔹 Floating Point Variables
All floating point types are **signed**.

```cpp
float x{};
double y{};
long double z{};
```
#### Literal Suffixes
```cpp
float num{ 3.14 };   // implicit double → float (narrowed)
float num{ 3.14f };  // explicit float
```

| Type          | Suffix  | Example  |
|---------------|---------|----------|
| `float`       | `f`     | `3.14f`  |
| `double`      | *(none)*| `3.14`   |
| `long double` | `l`     | `3.14l`  |

> 💡 Use `f` for float literals to avoid implicit promotion during arithmetic.

```cpp
float x{ 2.0f };
auto result = x * 3.0; // x is promoted to double, result is double
```

---
### 🔹 NaN and Inf

IEEE 754 compatible formats additionally support some special values:

- **Inf**, which represents infinity. Inf is signed, and can be positive (+Inf) or negative (-Inf).
- **NaN**, which stands for “Not a Number”. There are several different kinds of NaN (which we won’t discuss here).
- Signed zero, meaning there are separate representations for “positive zero” (+0.0) and “negative zero” (-0.0).

Formats that are not compatible with IEEE 754 may not support some (or any) of these values. In such cases, code that uses or generates these special values will produce implementation-defined behavior.
___
### 📌 Key Definitions
- **Floating Point Type**: C++ type for real numbers with decimals (e.g., `float`, `double`).
- **Precision**: The number of significant digits stored without loss.
- **Mantissa/Significand**: The binary digits of a number’s magnitude in scientific notation.
- **`std::setprecision(n)`**: Controls output precision (significant digits or decimal places).
- **`std::fixed`**: Switches output to fixed-point notation (decimal-focused).
- **Literal Suffix**: Suffix like `f`, `l` to specify the literal type (float, long double).

---

### 🧠 Flashcards

**Q:** What’s the default floating point type in C++ when you write `3.14`?  
**A:** `double`

**Q:** What does `std::setprecision(8)` control by default?  
**A:** Number of significant digits

**Q:** What suffix makes `3.14` a float literal?  
**A:** `f` (e.g., `3.14f`)

**Q:** What does `std::fixed` change about output?  
**A:** It causes `setprecision(n)` to control **digits after the decimal**.

**Q:** Why can’t `0.1` be stored exactly in binary?  
**A:** It’s not a clean base-2 fraction — binary representation is infinite.
