 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚8:30 pm  📆 Tue Sep 23
 🔗 **Related Concepts**: #note #cpp
___
## 📝 Note: Operator Precedence and Associativity
In mathematics, an *operation* is a process that takes one or more input values (called **operands**) and produces a result (called an output value). The symbol that represents the operation is known as the **operator**.

For example:
```txt
      2            +           2          =         4
  (operand)   (operator)   (operand)   (equals)  (result)
```
In math, the equals sign (`=`) is a **relational symbol**, not an operator, it simply states that the left and right sides are equal. In C++, however, operators form the building blocks of **expressions**. This note focuses on how those operators are evaluated, and why **precedence** and **associativity** are critical to understanding program behavior.
___
### 🔹 Evaluation of Compound expressions
Let's consider an extremely basic compound expression: $2 + 3 * 6$. In regular mathematics, we have system called **PEMDAS**, and it stands for **Parentheses, Exponent, Multiplication, Division, Addition, Subtraction**. If we follow those rules, this would get solved for $20$, meaning it would look something like this: $2 + (3 * 6)$. Although for C++, the compiler needs to do a few things.
1. At compile time, the compiler must parse the expression and determine how operands are grouped with operators. This is done via the precedence and associativity rules, which we'll discuss momentarily.
2. At compile time or runtime, the operands are evaluated and operations executed to produce a result.
#### Precedence and Associativity
- **Operator Precedence** is a system that assigns all operators a level of precedence. It's sort of like each operator has a specific level of importance and when the operator of the highest importance gets evaluated first.

Consider an expression, `7 - 4 - 1`. Obviously, with two subtraction operators, they must have the same level of precedence, so how does the compiler get this parsed? When this situation arises, where the compiler cannot depend on precedence alone, it uses *associativity*.

- **Associativity**: If two operators with the same precedence level are adjacent to each other in an expression, the operator's **associativity** tells the compiler whether to evaluate the operators (not operands!) from left to right or from right to left. In our example above, with all subtraction, it would be evaluated like this, `(7 - 4) - 1`.
##### Table of Operator Precedence and Associativity
|Prec/Ass|Operator|Description|Pattern|
|---|---|---|---|
|1 L->R|::  <br>::|Global scope (unary)  <br>Namespace scope (binary)|::name  <br>class_name::member_name|
|2 L->R|()  <br>()  <br>type()  <br>type{}  <br>[]  <br>.  <br>->  <br>++  <br>––  <br>typeid  <br>const_cast  <br>dynamic_cast  <br>reinterpret_cast  <br>static_cast  <br>sizeof…  <br>noexcept  <br>alignof|Parentheses  <br>Function call  <br>Functional cast  <br>List init temporary object (C++11)  <br>Array subscript  <br>Member access from object  <br>Member access from object ptr  <br>Post-increment  <br>Post-decrement  <br>Run-time type information  <br>Cast away const  <br>Run-time type-checked cast  <br>Cast one type to another  <br>Compile-time type-checked cast  <br>Get parameter pack size  <br>Compile-time exception check  <br>Get type alignment|(expression)  <br>function_name(arguments)  <br>type(expression)  <br>type{expression}  <br>pointer[expression]  <br>object.member_name  <br>object_pointer->member_name  <br>lvalue++  <br>lvalue––  <br>typeid(type) or typeid(expression)  <br>const_cast<type>(expression)  <br>dynamic_cast<type>(expression)  <br>reinterpret_cast<type>(expression)  <br>static_cast<type>(expression)  <br>sizeof…(expression)  <br>noexcept(expression)  <br>alignof(type)|
|3 R->L|+  <br>-  <br>++  <br>––  <br>!  <br>not  <br>~  <br>(type)  <br>sizeof  <br>co_await  <br>&  <br>*  <br>new  <br>new[]  <br>delete  <br>delete[]|Unary plus  <br>Unary minus  <br>Pre-increment  <br>Pre-decrement  <br>Logical NOT  <br>Logical NOT  <br>Bitwise NOT  <br>C-style cast  <br>Size in bytes  <br>Await asynchronous call  <br>Address of  <br>Dereference  <br>Dynamic memory allocation  <br>Dynamic array allocation  <br>Dynamic memory deletion  <br>Dynamic array deletion|+expression  <br>-expression  <br>++lvalue  <br>––lvalue  <br>!expression  <br>not expression  <br>~expression  <br>(new_type)expression  <br>sizeof(type) or sizeof(expression)  <br>co_await expression (C++20)  <br>&lvalue  <br>*expression  <br>new type  <br>new type[expression]  <br>delete pointer  <br>delete[] pointer|
|4 L->R|->*  <br>.*|Member pointer selector  <br>Member object selector|object_pointer->*pointer_to_member  <br>object.*pointer_to_member|
|5 L->R|*  <br>/  <br>%|Multiplication  <br>Division  <br>Remainder|expression * expression  <br>expression / expression  <br>expression % expression|
|6 L->R|+  <br>-|Addition  <br>Subtraction|expression + expression  <br>expression - expression|
|7 L->R|<<  <br>>>|Bitwise shift left / Insertion  <br>Bitwise shift right / Extraction|expression << expression  <br>expression >> expression|
|8 L->R|<=>|Three-way comparison (C++20)|expression <=> expression|
|9 L->R|<  <br><=  <br>>  <br>>=|Comparison less than  <br>Comparison less than or equals  <br>Comparison greater than  <br>Comparison greater than or equals|expression < expression  <br>expression <= expression  <br>expression > expression  <br>expression >= expression|
|10 L->R|==  <br>!=|Equality  <br>Inequality|expression == expression  <br>expression != expression|
|11 L->R|&|Bitwise AND|expression & expression|
|12 L->R|^|Bitwise XOR|expression ^ expression|
|13 L->R|\||Bitwise OR|expression \| expression|
|14 L->R|&&  <br>and|Logical AND  <br>Logical AND|expression && expression  <br>expression and expression|
|15 L->R|\|  <br>or|Logical OR  <br>Logical OR|expression \| expression  <br>expression or expression|
|16 R->L|throw  <br>co_yield  <br>?:  <br>=  <br>*=  <br>/=  <br>%=  <br>+=  <br>-=  <br><<=  <br>>>=  <br>&=  <br>\|=  <br>^=|Throw expression  <br>Yield expression (C++20)  <br>Conditional  <br>Assignment  <br>Multiplication assignment  <br>Division assignment  <br>Remainder assignment  <br>Addition assignment  <br>Subtraction assignment  <br>Bitwise shift left assignment  <br>Bitwise shift right assignment  <br>Bitwise AND assignment  <br>Bitwise OR assignment  <br>Bitwise XOR assignment|throw expression  <br>co_yield expression  <br>expression ? expression : expression  <br>lvalue = expression  <br>lvalue *= expression  <br>lvalue /= expression  <br>lvalue %= expression  <br>lvalue += expression  <br>lvalue -= expression  <br>lvalue <<= expression  <br>lvalue >>= expression  <br>lvalue &= expression  <br>lvalue \|= expression  <br>lvalue ^= expression|
|17 L->R|,|Comma operator|expression, expression|
==Note: C++ **Does Not** include an operator to do exponentiation (operator^ has a different function in C++). We discuss exponentiation more in later.==
___
### 🔹 Best Practices & Notable Thoughts
 - Due to the rules of precedence `4 + 2 * 3` will be grouped as `4 + (2 * 3)`, but what if we *actually* meant `(4 + 2) * 3`? Well, just like in regular mathematics, use parentheses to express intent.
 - Expressions with a single assignment operator do not need to have the operand of the assignment wrapped in parenthesis.
 - Operands, function arguments, and subexpressions may be evaluated in any order.
 - Value computation is the formal term used to mean the execution of operators in an expression to produce a value.
___
### 🧠 Flashcards

   
In mathematics, what role does `=` serve in an expression like `2 + 2 = 4`?   
?|?  
It is a **relational symbol** that asserts equality, not an operator performing an action.

---


In C++, what does the `=` symbol represent?   
?|?  
The **assignment operator**, which stores the value on the right into the variable on the left.

---


What determines the order in which different operators in a compound expression are grouped?  
?|?  
**Precedence rules**.

---


What resolves ambiguity when two operators of the same precedence appear next to each other in an expression?  
Answer  
?|?  
**Associativity**, which specifies left-to-right or right-to-left grouping.

---

Given `7 - 4 - 1`, how does associativity affect evaluation?  
?|?  
Subtraction is **left-associative**, so it’s grouped as `(7 - 4) - 1`.

---


What’s the result of `4 + 2 * 3` in C++ and why?  
?|?  
`10`, because multiplication has higher precedence, so it’s grouped as `4 + (2 * 3)`.

---

How can you override operator precedence in an expression?  
?|?  
By using **parentheses** to explicitly define grouping.

---


Do precedence and associativity determine the order in which operands are evaluated?    
?|?  
❌ No. Operands and subexpressions may be evaluated in **any order**, which can lead to undefined behavior if side effects are involved.

---


What is the formal term for executing operators in an expression to produce a result?  
?|?  
**Value computation**.

---

Why is relying solely on precedence a bad practice in complex expressions?  
?|?  
It makes code harder to read and can produce unintended results — **parentheses should be used to clarify intent**.


#flashcards 