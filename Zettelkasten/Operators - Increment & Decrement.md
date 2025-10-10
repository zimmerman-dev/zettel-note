 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚6:28 pm  📆 Fri Sep 26
 🔗 **Related Concepts**: #note #cpp  [[Operators - Overview]] , [[Operators - Arithmetic, Remainder, and Exponentiation]] , [[Control Flow - Overview]] , [[Control Flow - For Loop]] [[Operators - Precedence and Associativity]]
___
## 📝 Note: Operators - Increment & Decrement
Increment (`++`) and decrement (`--`) operators increase or decrease a value by one. Though they look simple, they behave differently depending on where they appear in an expression.
- `++`: adds `1` to an object.
- `--`: subtracts `1` from an object.
#### Are they arithmetic or assignment?
They’re technically **unary operators**—not assignment operators—but they do **perform arithmetic** and then **assign the result** back to the variable.
___
### `i++` vs `++i`
Depending on whether the operator comes **before or after** the variable, it behaves differently.
- Post-increment: `i++` - This means the increment happens after the object is *used*.
- Pre-increment: `++i` - This means the increment happens before the object is *used*.

**Example**:
```cpp
#include <iostream>

int main() {
  
  int i{3};
  int x{3};
  
  std::cout << i << " , " << x << std::endl;
  std::cout << i++ << " , " << ++x << std::endl;
  std::cout << i++ << " , " << ++x << std::endl;
  std::cout << i << " , " << x << std::endl;
  
  return 0;
}
```
> Before you run this program, what do you think it will be?

Output:
```text
3 , 3
3 , 4
4 , 5
5 , 5
```
### 🔹 The 🚥 Signal Model: Visualizing ++ and --
When you're using increment/decrement inside a **larger expression**, it's important to understand **when the value is read** versus **when the variable is modified**. This is where many bugs creep in.
___
--- start-multi-column: ID_aa58
```column-settings
Number of Columns: 3
Largest Column: Standard
Column Spacing: 3px
Overflow: Hidden
Border: off
```
#### The Signal Model
This model is to help you visualize confusing increment/decrement problems.

| Expression |   Signal   |       What happens        | When it's visible |
| :--------: | :--------: | :-----------------------: | :---------------: |
|   `++x`    | 🟢 Prefix  | Increment first, then use |   New value now   |
|   `x++`    | 🟡 Postfix | Use first, then increment |  New value later  |
**Rule of Thumb**:
> Use prefix when you want the updated value immediately.  
> Use postfix when you want the current value first, and the update to happen after.

--- column-break ---
#### Breaking Down Complex Expressions
Expressions like this:
```cpp
int x{4};
int y = ++x + x++ + x;
```
...can look confusing, but you can break them into steps like this:

1. **`++x`** (🟢): `x = 5`, use `5`
2. **`x++`** (🟡): use `5`, then `x = 6`
3. **`x`**: read current `x` = `6`

**Final**:
```cpp
y = 5 + 5 + 6 = 16
x = 6
```

--- column-break ---
#### Mental Insight 
If you are ever confused, imagine writing each part on its own line, like:
```cpp
int first = ++x;
int second = x++;
int third = x;
int y = first + second + third;
```
>It’s like running through the expression as if each part was on its own line. Even though it _looks_ like one expression, each segment modifies the original variable, and each one has its own timing for when the value is read vs updated.

This trick makes it feel **atomic and step-by-step**, which is exactly how the compiler sees it.

--- end-multi-column
___
### 🔹 Common Use Cases and Side Effects
Most often used in **loops**: 
```cpp
for (int i = 0; i < 10; ++i) {
... }
```  
- Can be used in any context where a variable is being modified by 1.
- Yes, they can be used **outside loops**, but they should be used carefully in expressions to avoid ambiguity.
  #### Expression Side Effects
Inside complex expressions, `++` and `--` can be error-prone:
```cpp
int x = 5;
int y = x++ + ++x;  // Order of operations can be unclear
```
While problems like these serve as good puzzles for practicing your understanding of these operators, **Avoid using the same variable more than once in an expression involving `++` or `--`** in real production code.
___
### 🔹 When _not_ to use them
- Don’t use `x++` or `--x` more than once in a single expression.
- Avoid complex expressions where the evaluation order isn't obvious.
- In performance-sensitive code (e.g., iterators), prefer `++i` over `i++`:
    - `++i` is often slightly faster because it doesn’t create a temporary copy (for user-defined types like iterators).
___
### 🧠 Flashcards

What is the key difference between prefix (`++i`) and postfix (`i++`) increment?  
?|?  
Prefix modifies the variable _before_ it is used in the expression; postfix uses the current value and increments _after_.

---

In this code, what is the value of `b`?

```cpp
int a{3}; 
int b = ++a;
```
?|?  
`b = 4`. The prefix increment increases `a` to 4 before the assignment.

---

What does this print?
```cpp
int x{4}; 
int y = ++x + x++ + x; 
std::cout << "x: " << x << ", y: " << y;
```
?|?  
`x: 6, y: 16`.
- `++x` → 5  
- `x++` → 5, then x becomes 6   
- final x → 6   
- `y = 5 + 5 + 6 = 16`

---

What is the danger of writing code like this?

```cpp
int y = a++ + a++;
```
?|?  
This causes **undefined behavior** because `a` is modified more than once in a single expression without a sequence point. Never do this in real code.

---

How can you safely rewrite this to avoid side effects?

```cpp
int y = ++x + x++ + x;
```
?|?  
Break it into separate lines:
```cpp
int first = ++x; 
int second = x++; 
int third = x; 
int y = first + second + third;
```

---

What’s the rule of thumb for using increment/decrement in expressions?  
?|?  
Avoid using the same variable more than once in an expression involving `++` or `--`. It’s safer and more readable to separate side effects from logic.

#flashcards 