 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚9:51 pm  📆 Fri Sep 26
 🔗 **Related Concepts**: #note #cpp [[Operators - Overview]] , [[Operators - Precedence and Associativity]] , [[Operators - Arithmetic, Remainder, and Exponentiation]] , [[Conditionals]] , [[Introduction to if-else]]
___
## 📝 Note: Operators - Relational & Logical
**Relational Operators**: are operators that evaluate two values, and check whether a condition is true or false.
**Logical Operators**: are operators that can compare multiple values to test multiple conditions.
--- start-multi-column: ID_tyar
```column-settings
Number of Columns: 2
Largest Column: Standard
Column Spacing: 3px
Border: off
Overflow: Hidden
```
#### Relational Operators
C++ provides six relational operators used for comparisons:

|        Operator        | Symbol |   Form   |                              Operation                               |
| :--------------------: | :----: | :------: | :------------------------------------------------------------------: |
|      Greater than      |  `>`   | `x > y`  |       `true` if `x` is **greater than** `y`, `false` otherwise       |
|       Less Than        |  `<`   | `x < y`  |        `true` if `x` is **less than** `y`, `false` otherwise         |
| Greater than or equals |  `>=`  | `x >= y` | `true` if `x` is **greater than or equal** to `y`, `false` otherwise |
|  Less than or equals   |  `<=`  | `x <= y` |  `true` if `x` is **less than or equal** to `y`, `false` otherwise   |
|        Equality        |  `==`  | `x == y` |          `true` if `x` is **equals** `y`, `false` otherwise          |
|       Inequality       |  `!=`  | `x != y` |        `true` if `x` does **not equal** `y`, false otherwise         |
Relational operators are fairly intuitive as they all evaluate to the Boolean true value `1`, or false `0`. This is why you can visualize relational operators like this:
```cpp
     if (x == true)                 |            if (x == false)
/*   is the same thing as:    */    |   /*       is the same thing as:    */
     if (x)                         |            if (!x)
```
#### Comparison with floating point values
Considering the fact that floating point values are inherently imprecise, comparisons can be quite hard. Less than and greater than comparisons *can* be accomplished, but equality and inequality is much more troublesome. The smallest rounding error will cause `==` to fail. Instead, use an epsilon comparison:
```cpp
#include <cmath>
if (std::abs(a - b) < epsilon) { /* close enough */ }
```
See: [[cmath]]

--- column-break ---
#### Logical Operators
C++ provides 3 logical operators where you can test multiple conditions at once. See: [[Boolean Logic]] and [[Gates]] for more practical information.

|  Operator   | Symbol |     Form     |                              Operation                              |
| :---------: | :----: | :----------: | :-----------------------------------------------------------------: |
| Logical NOT |  `!`   |     `!x`     |        `true` if `x` is `false`, or `false` if `x` is `true`        |
| Logical AND |  `&&`  |   `x && y`   |      `true` if `x` and `y` are both `true`, `false` otherwise       |
| Logical OR  |  \|\|  | `x` \|\| `y` | `true` if either (or both) `x` *or* `y` are true, `false` otherwise |
##### Logical NOT `!`
```text
| Operand | Result |
|---------|--------|
|  true   |  false |
|  false  |  true  |
```
- If *logical NOT's* **operand** evaluates to `true`, *logical NOT* evaluates to `false`.
- if *logical NOT's* **operand** evaluates to `false`, *logical NOT* evaluates to `true`.


--- end-multi-column

































___
### 📌 Key Definitions










___
### 🧠 Flashcards

