#### 📝 Note: Increment and Decrement
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚ 11:36 pm  🗓️: Tue Jul 22
 🔗 **Related Concepts**: #cpp #note [[Operators]] , [[Statements and Expressions]] , [[Operator Overloading]] , [[Loops]] , [[Conditionals]] , [[Jump Statements]]

___
## ➕➖ Increment and Decrement Operators

Increment (`++`) and decrement (`--`) operators increase or decrease a value by one. Though they look simple, they behave differently depending on where they appear in an expression.

### 📚 What are they?

- `++` adds one to a variable.
- `--` subtracts one from a variable.
#### Syntax:

```cpp
i++;   // post-increment
++i;   // pre-increment

i--;   // post-decrement
--i;   // pre-decrement
```
#### Are they arithmetic or assignment?

They’re technically **unary operators**—not assignment operators—but they do **perform arithmetic** and then **assign the result** back to the variable.

---
### ⚙️ Prefix vs Postfix

#### What’s the difference?
- `++x`: pre-increment happens **before** the value is used

```cpp
sum = ++num;
// Means:
num = num + 1;
sum = num;
```

- `x++`: post-increment happens **after** the value is used

```cpp
sum = num++;
// Means:
sum = num;
num = num + 1;
```



Prefix vs Postfix – Execution Breakdown

```cpp

Let's say:
    int num = 10;
    int sum;

⚙️ Pre-Increment ( ++num )
--------------------------
sum = ++num;

Step-by-step:
1. num is incremented → num becomes 11
2. sum is assigned the new value of num → sum = 11

Final values:
    num = 11
    sum = 11


⚙️ Post-Increment ( num++ )
---------------------------
sum = num++;

Step-by-step:
1. sum is assigned the current value of num → sum = 10
2. num is incremented → num becomes 11

Final values:
    num = 11
    sum = 10

🧠 Rule of Thumb:
- Pre-increment (++x): "Increment *then* use"
- Post-increment (x++): "Use *then* increment"
- The result affects the expression it's used in, not the whole statement.
```

### 🔁 Common Use Cases

- Most often used in **loops**:

    ```cpp
    `for (int i = 0; i < 10; ++i) { ... }`
``  ```  

- Can be used in any context where a variable is being modified by 1.
- Yes, they can be used **outside loops**, but they should be used carefully in expressions to avoid ambiguity.

---
## 🧠 Expression Side Effects

- Inside complex expressions, `++` and `--` can be error-prone:
    ```cpp
    int x = 5;
    int y = x++ + ++x;  // Order of operations can be unclear
```

- **Avoid using the same variable more than once in an expression involving `++` or `--`.**

### 👷‍♂️ Can they be overloaded?

Yes—C++ allows you to define `++` and `--` for your own classes.

#### Syntax:
```cpp
MyClass& operator++();       // Prefix
MyClass operator++(int);     // Postfix — note the `int` is just a dummy parameter
```

---
### ❌ When _not_ to use them

- Don’t use `x++` or `--x` more than once in a single expression.
- Avoid complex expressions where the evaluation order isn't obvious.
- In performance-sensitive code (e.g., iterators), prefer `++i` over `i++`:
    - `++i` is often slightly faster because it doesn’t create a temporary copy (for user-defined types like iterators).