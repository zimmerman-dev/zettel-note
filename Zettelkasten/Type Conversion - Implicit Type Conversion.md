 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚3:13 pm  📆 Sat Sep 13
 🔗 **Related Concepts**: #note #cpp [[Type Conversion - Overview]] [[Type Conversion - Type Casting & static_cast]]
___
## 📝 Note: Type Conversion - Implicit Type Conversion
### Example 1
Consider the following program:
```cpp
#include <iostream>

void print(double x) {
  std::cout << x << '\n';
}

int main() {

  int num{ 5 };
  print(num);

  return 0;
}
```

Output:
```bash
5
```
Here's a question. is  the output 5 an `int`, or `double`? If you're unsure, run the first program in the debugger, and add both `num` and `x` to the watch window in your debugger. When you're done, add this line to the function to check your answer:

```cpp
void print(double x) {
  std::cout << x << '\n';
  std::cout << typeid(x).name(); // This line will tell you the type of 'x'.
}
```
___
### 🔹 Implicit Type Conversion
In the above example, the `print()` function has a parameter type `double`, but the caller is passing an `int`.

C++ allows many fundamental types to be **implicitly converted** into others when needed. Here, the compiler sees an `int` being passed into a function expecting a `double`, so it quietly creates a temporary `double` holding the value `5`.

#### Key insight
The original object (`num`) stays an `int`. The compiler just uses its value to create a **temporary of the target type** (`double`) for the function call. This is why implicit conversion behaves much like pass-by-value: the function gets a separate copy in the converted type, and the caller’s variable is unchanged.

#### Example 2
While implicit type conversion is sufficient for most cases where type conversion is needed, there are a few cases where it is not. Consider the following program:
```cpp
#include <iostream>

void print(int x) {
  std::cout << x << '\n';
}

int main() {

  print(5.3);
  return 0;
}
```
#### Output

```bash
5
```
Similar to first example, **implicit type conversion** happens here as well. The difference between them is that the first example performs a **widening** conversion (`int` to `double`) — generally safe. This one does the opposite: a **narrowing** conversion (`double` to `int`), which can lose data.

#### Truncation
Notice how the output is `5`, rather than `5.3`. This happens because, as we know from our earlier notes on integer types, integer types **cannot** hold fractional parts.

You might have thought that upon an implicit type conversion from `float` to `int`,  it is rounding down to `5`. This is not the case. What happens is what is referred to as **truncation** . Rather than rounding, whatever is after the decimal point is cut off.  Even in the case of the number being `5.99999` before the type conversion, the number will be truncated to just `5`.

This is why implicit type conversions from `int` to `float` are generally safe, while `float` to `int` can lose precision.”
___
### TL;DR Summary
C++ allows implicit conversions between arithmetic types. When converting from a type that can represent fewer values to one that can represent more (like `int` → `double`), this is often informally called a **widening conversion**.
Going from a type that can represent more values to one that can represent fewer (`double` → `int`) is called a **narrowing conversion** — and may result in loss of data (e.g. truncation). For reference here's a table of **common implicit conversions**:

| From     | To       | Safe?  | Notes                          |
|----------|----------|--------|-------------------------------|
| `int`    | `double` | ✅     | Widening — no data loss       |
| `double` | `int`    | ⚠️     | Narrowing — fractional part lost (truncation) |
| `char`   | `int`    | ✅     | Used in ASCII manipulation    |
| `bool`   | `int`    | ✅     | `true → 1`, `false → 0`       |
| `int`    | `bool`   | ⚠️     | `0 → false`, others → true    |

___
### Explicit Type Conversion
What if we wanted to *intentionally* convert a value from one type to another? With our last example, what if we wanted to do an **explicit type conversion** from `double` to `int`, truncation and all? If that's the case, we would want to show intent in code.
```cpp
#include <iostream>

void print(int x) {
  std::cout << x << '\n';
}

int main() {
  double num{5.5};
  print(static_cast<int>(num));

  return 0;
}
```
Because we are now explicitly  requesting that `double` value to be converted to an `int` value, the compiler won't generate any warnings about possible loss of data, and it shows intent for whoever else may be working on our codebase.
___
### Use Cases and Caveats for `static_cast`
- Signed and unsigned conversions: `static_cast` can be used to convert signed values to unsigned (and vice-versa). This preserves the bit pattern but changes how the value is interpreted, often resulting in large numbers when negative values are cast to unsigned.
	- - **Pre-C++20 behavior**: Converting an unsigned value to a signed type was implementation-defined **if the value couldn't be represented in the signed type**.


- in our note [[fixed-width integers]] we learn how `std::int8_t` may behave like a char on most systems. If you want to be sure it is treated like an integer, you can cast it as such.

#### Reminders
- By default, floating point values whose value decimal part is 0 without decimal places (e.g. `5.0` prints as `5`).
- Implicit conversions where you narrow from double to int will most likely throw compiler warnings. For testing purposes, you have to disable, "_treat warnings as errors_" but I wouldn't recommend keeping that disabled. It's much better to use static_cast if you intend to perform an unsafe conversion.
___

### 📌 Key Definitions

- **Implicit type conversion**: Automatic conversion performed by the compiler when types don’t match but are compatible.
- **Explicit type conversion**: Manual type conversion using a cast (e.g., `static_cast`), which shows programmer intent.
- **Truncation**: When converting a floating-point value to an integer, the fractional part is discarded (not rounded).
___
### 🧠 Flashcards

**Q:** What is _implicit type conversion_ in C++?
**A:** Automatic conversion performed by the compiler when types don’t match but are compatible (e.g. passing `int` to a function expecting `double`).

----------

**Q:** Does the following function receive an `int` or a `double`?

```cpp
void print(double x) {
  std::cout << x << '\n';
}
int main() {
  int num{ 5 };
  print(num);
}

```

**A:** It receives a `double`. The `int` is implicitly converted to a temporary `double` during the function call.

----------

**Q:** What’s the output of this program, and why?

```cpp
void print(int x) {
  std::cout << x << '\n';
}
int main() {
  print(5.9999);
}

```

**A:** Output: `5`. The `double` is implicitly converted to `int` by _truncation_, not rounding.

----------

**Q:** What's the difference between _widening_ and _narrowing_ conversions in C++?
**A:** Widening (e.g. `int → double`) increases range and is generally safe. Narrowing (e.g. `double → int`) loses information (e.g. fractional part) and can be unsafe.

----------

**Q:** Why is `static_cast` preferred over implicit conversion for narrowing types?
**A:** It shows clear intent, avoids compiler warnings, and signals that data loss is deliberate.

----------

**Q:** What happens when casting a negative signed int to `unsigned int` using `static_cast`?
**A:** The bit pattern is preserved, but the result becomes a large positive number due to modulo conversion (e.g., `static_cast<unsigned>(-1)` → `4294967295` on 32-bit).

----------

**Q:** True or False: Converting an out-of-range `unsigned int` to `int` was well-defined before C++20.
**A:** False. It was _implementation-defined_ prior to C++20.

#flashcards 