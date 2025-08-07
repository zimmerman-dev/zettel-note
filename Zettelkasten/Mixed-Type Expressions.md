#### 📝 Note: Mixed-Type Expressions 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚12:31 am  📆 Thu Jul 24
 🔗 **Related Concepts**: #cpp #note [[Statements and Expressions]] , [[Data Types]] , [[C++ Syntax Reference]] , [[Type Casting]] 
___
### 🎭 Mixed-Type Expressions

An expression involving **two or more different day types**, such as `int` and `double`.
**Example:**

- C++ operations occur on same type operands
- If operands are of different types, C++ will convert one
- Important! since it could affect calculation results
- C++ will attempt to automatically convert types (coercion). If it can't, a compiler error will occur.

### 🔄 Type Conversions 

>[!note] What is it?
>- Type conversion means **changing a value from one type to another.**
>- This happens all the time in C++ when you're doing math with different kinds of numbers.

### 🔺Higher vs Lower Types

Higher vs. Lower Types are based on the size of the values the **type** can hold. When C++ has to choose, it will **convert lower types to higher ones** to keep things safe.

- `double` is **higher** than `int` (it can store decimals and bigger numbers)
- `int` is **higher** than `char` (it holds bigger numbers)
- `unsigned int` and `signed int` are at the same "size" but behave differently.

```cpp title:Example
int a {5};
double b {2.0};
auto result = a + b; //result is promoted to double
```

- `int` (`a`) is the lower type
- `double` (`b`) is the higher type
- C++ *converts* `a` into a `double` automatically (**coercion**) so they match.

---
### 🌀 Type Coercion 

As state above, **Type Coercion** just means that *C++ automatically (at compile time) converts one type into another without you doing anything.*

**Promotion:** Converting to a higher type, i.e., `int -> double`, `char -> int`, etc.
- Used in mathematical expressions.

```cpp title:Promotion
// lower op higher
2 * 5.2; // (2 is promoted to 2.0) The lower is promoted to a higher
```

**Demotion:** Converting to a lower type, i.e., `double -> int` (*may* lose data!)
- Used with assignment to lower type.

```cpp title:Demotion
// lower = hgher
int nmum {0}; // The higher is demoted to a lower
num = 100.2;
```

### 🚧 Types Hierarchy

Diagram for visual aid on types hierarchy for promotion and demotion here:
[[Types Hierarchy]]

---
### 🌡️ Type Casting

Continued: 
[[Type Casting]]
