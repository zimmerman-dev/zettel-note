 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚9:51 pm  📆 Fri Sep 26
 🔗 **Related Concepts**: #note #cpp [[Operators - Overview]] , [[Operators - Precedence and Associativity]] , [[Operators - Arithmetic, Remainder, and Exponentiation]] , [[Conditionals]] , [[Introduction to if-else]]
___
## 📝 Note: Operators - Relational & Logical
**Relational operators** compare two values and return a Boolean result (`true` or `false`). 
**Logical operators** are used to combine or modify boolean expressions, which are expressions that evaluate to either `true` or `false`.
--- start-multi-column: ID_tyar
```column-settings
Number of Columns: 2
Largest Column: Standard
Column Spacing: 3px
Border: off
Overflow: Hidden
```
### 🔹 Relational Operators
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

--- column-break ---
#### Comparison with floating point values
Considering the fact that floating point values are inherently imprecise, comparisons can be quite hard. Less than and greater than comparisons *can* be accomplished, but equality and inequality is much more troublesome. The smallest rounding error will cause `==` to fail. 
```cpp
std::cout << std::boolalpha << (0.3 == 0.2 + 0.1); // prints false
```

Instead, use an **epsilon** comparison. See: [[Floating-Point Math]] for an in depth understanding of epsilon.
```cpp
if (std::abs(a - b) < epsilon) { /* close enough */ }
```

--- end-multi-column
___
### 🔹 Logical Operators
C++ provides 3 logical operators where you can test multiple conditions at once. See: [[Boolean Logic]] and [[Logic Gates]] for more practical information.

|  Operator   | Symbol |     Form     |                              Operation                              |
| :---------: | :----: | :----------: | :-----------------------------------------------------------------: |
| Logical NOT |  `!`   |     `!x`     |        `true` if `x` is `false`, or `false` if `x` is `true`        |
| Logical AND |  `&&`  |   `x && y`   |      `true` if `x` and `y` are both `true`, `false` otherwise       |
| Logical OR  |  \|\|  | `x` \|\| `y` | `true` if either (or both) `x` *or* `y` are true, `false` otherwise |
--- start-multi-column: ID_byv6
```column-settings
Number of Columns: 3
Largest Column: Standard
Column Spacing: 3px
Border: off
Overflow: Hidden
```
#### Logical NOT `!`
The *logical NOT* inverts Boolean conditions. Truth table:

| Operand | Result  |
| :-----: | :-----: |
| `true`  | `false` |
| `false` | `true`  |
- If *logical NOT's* **operand** evaluates to `true`, *logical NOT* evaluates to `false`.
- if *logical NOT's* **operand** evaluates to `false`, *logical NOT* evaluates to `true`.

**Best Practice**:
> If *logical NOT* is intended to operate on the result of other operators, the other operators and their operands need to be enclosed in parentheses due its very high precedence.

--- column-break ---
#### Logical OR `||`
The *logical OR* operator is used to test whether either of two conditions is `true`. Truth table:

| Left Operand | Right Operand | Result  |
| :----------: | :-----------: | :-----: |
|   `false`    |    `false`    | `false` |
|    `true`    |    `false`    | `true`  |
|   `false`    |    `true`     | `true`  |
|    `true`    |    `true`     | `true`  |
- If *logical OR's* **left operand** evaluates to `false`, and **right operand** evaluates to `false`, *logical NOT* returns `false`.
- If *logical OR's* **left operand** evaluates to `false`, and **right operand** evaluates to `true`, *logical NOT* returns `true`.
- If *logical OR's* **left operand** evaluates to `true`, and **right operand** evaluates to `false`, *logical NOT* returns `true`.
- If *logical OR's* **left operand** evaluates to `true`, and **right operand** evaluates to `true`, *logical NOT* returns `true`.

--- column-break ---
#### Logical AND `&&`
The *logical AND* operator is used to test whether both operands are `true`. If both are `true`, Logical AND returns `true`. Truth table:

| Left Operand | Right  Operand | Result  |
| :----------: | :------------: | :-----: |
|   `false`    |    `false`     | `false` |
|    `true`    |    `false`     | `false` |
|   `false`    |     `true`     | `false` |
|    `true`    |     `true`     | `true`  |
- If *logical AND's* **left operand** evaluates to `false`, and **right operand** evaluates to `false`, *logical AND* returns `false`.
- If *logical AND's* **left operand** evaluates to `true`, and **right operand** evaluates to `false`, *logical AND* returns `false`.
- If *logical AND's* **left operand** evaluates to `false`, and **right operand** evaluates to `true`, *logical AND* returns `false`.
- If *logical AND's* **left operand** evaluates to `true`, and **right operand** evaluates to `true`, *logical AND* returns `true`.

--- end-multi-column
### 🔹Short-Circuit Evaluation
For optimization purposes, C++ has a system that called **short-circuit evaluation**. In general, the way it works is this:

- In order for an `&&` operator to evaluate both sides of the expression, the left side operand has to be `true`. This is because, if you look at the truth table, if only one side is `false`, the compound expression evaluates to `false`. Hence, the compiler assumes that evaluating the rest of the expression is unnecessary because one side has already evaluated as `false`.

- Equally for the `||` operator, if the first operand evaluates as `true`, it will skip the second condition and evaluate the entire compound expression as `true`. Again, look at the truth table. See how whether you have one or either side evaluating as `true`, the whole compound expression will evaluate `true`.

> 💡 **Tip**: The left-hand operand of a logical expression may prevent the right-hand side from being evaluated.
___
### 🔹 Mixing `&&` and `||`
Mixing *logical AND* and *logical OR* in the same expression often **cannot** be avoided, but it is an area you should tread with great caution. Because the logical operators are all grouped together categorically, many new programmers assume they have the same level of precedence. This is not so:

**Precedence**:
`!`  ---> `&&`  ---> `||`

Similar to the best practice note for the logical OR, one should generally use parentheses to clearly demonstrate your intentions in how an expression should order it's evaluations.
___
### 🧠 Flashcards

What does a relational operator return?  
?|?  
A Boolean value: `true` (1) or `false` (0)

---

What does the expression `x < y` evaluate to if `x` is 2 and `y` is 5?  
?|?  
`true` (1), because 2 is less than 5

---

How can you compare floating-point values reliably in C++?  
?|?  
Use an epsilon comparison: `std::abs(a - b) < epsilon`

---

What is the output of this code?

```cpp
std::cout << std::boolalpha << (0.3 == 0.2 + 0.1);
```

?|?  
`false` — due to floating-point imprecision

---

What is the symbol and function of the relational operator that checks inequality?  
?|?  
`!=` — it returns `true` if the two values are **not equal**

---

What is the result of `!true`?  
?|?  
`false`

---

What is the result of `true && false`?  
?|?  
`false`

---

What is the result of `false || true`?  
?|?  
`true`

---

What is the precedence order of the three logical operators?  
?|?  
`!` > `&&` > `||`

---

Why should you use parentheses when mixing `&&` and `||`?  
?|?  
To avoid mistakes caused by misunderstanding precedence; parentheses make the logic explicit

---

What does short-circuiting mean in `x && y`?  
?|?  
If `x` is `false`, `y` is not evaluated because the whole expression must be `false`

---

What does short-circuiting mean in `x || y`?  
?|?  
If `x` is `true`, `y` is skipped because the whole expression is already `true`

#flashcards 