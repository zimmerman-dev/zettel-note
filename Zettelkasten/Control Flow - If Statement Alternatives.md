 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚7:31 pm  📆 Thu Oct 9
 🔗 **Related Concepts**: #note #cpp [[Control Flow - Overview]] , [[Control Flow - Conditional Statements Overview]]
___
## 📝 Note: Control Flow - If Statement Alternatives
Although you could chain together an infinite amount of `if-else` statements (not literally), this is both inefficient and hard to read.
--- start-multi-column: ID_gayy
```column-settings
Number of Columns: 2
Largest Column: Standard
Column Spacing: 3px
Border: off
Overflow: Hidden
```
### 🔹`if` Recap
Consider the following program:
```cpp
#include <iostream>

void printSomething(int x) {
  if (x == 1) {
    std::cout << "One";
  } else if (x == 2) {
    std::cout << "Two";
  } else if (x == 3) {
    std::cout << "Three";
  } else {
    std::cout << "Unknown";
  }
}

int main() {
  printSomething(2);
  std::cout << '\n';

  return 0;
}
```
> Variable `x` in `printSomething()` gets evaluated up to three times depending on the value passed in (inefficiently), and the reader has to be sure that it is `x` being evaluated each time (not some other variable).

--- column-break ---
### 🔹 `switch` Statement
Testing an object for equality against a set of different values is common, so C++ provides an alternative conditional statement called a `switch` statement that is specialized for this purpose. Let's rewrite our function above and then we can go through the mechanics.
```cpp
// ...
void printSomething(int x) {
  switch (x) {
    case 1:
      std::cout << "One";
      return;
    
    case 2:
      std::cout << "Two";
      return;
    
    case 3:
      std::cout << "Three";
      return;
    
    default:
      std::cout << "Unknown";
      return;
  }
}
// ...
```

The idea behind the **switch statement** is that an expression (or condition) is evaluated to produce a value. Then one of the following happens:
- If the expression's value is equal to the value after any of the case labels, the statements after the matching case-label are executed.
- If no matching value is found and a default-label exists, the statements after the default-label are executed.
- If no matching value is found and there is no default-label, the switch is skipped.

--- end-multi-column
### 🔹 `switch` Dissected
As we have seen already, to start a `switch` statement, you start by using the `switch` keyword, followed by parentheses. Inside the parentheses it is usually a single variable or value, but it can be any **valid expression** (any expression that evaluated to an **integral type** or **enumerated type**). Following the `switch` expression, we declare a block, and inside we use labels to define all of the values we want to test for equality.
##### Why Only Integral Types?
Why are only integral (or enumerated) types allowed in `switch`? This is because `switch` statements are meant to be highly optimized. While compiler don't have to (and C++ doesn't always), the most common way for compilers to implement `switch` statements historically is via **jump table**, and jump tables only work with integral values. 
--- start-multi-column: ID_7o1g
```column-settings
Number of Columns: 3
Largest Column: Standard
Column Spacing: 3px
Border: off
Overflow: Hidden
```
#### Case Label
The first kind of label, declared using the `case` keyword and followed by a constant expression. The constant expression must either match the type of the condition or must be convertible to that type. If the value from the `switch` statement equals the expression after a `case` label, execution begins at the first statement after that `case` label and then continues sequentially.

--- column-break ---
#### Default Label
The second kind of label us the **default label** (often called the **default case**), which is declared using the `default` keyword. It is sort of similar to an `else` statement, only in that it acts as a sort of catch all if the `switch` statement expression does not equal any of the `case` labels. The `default` label *is* optional, and there can only be one `default` label per `switch` statement. By convention, it's always placed last in the `switch` block.

--- column-break ---
#### No `case`, No `default`?
If the value of the `switch` statement expression does not match any of the `case` labels, and `default` case has been provided, then no cases inside the `switch` are executed. **Execution path** continues after the end of the `switch` block.

--- end-multi-column
___
### 🔹`break` and `return`
In the above examples, we used `return` to stop execution after each case label. This served a dual purpose:

- It exited the `switch` statement once a match was found
- And it exited the **entire function**

But what if you're writing a `switch` inside the `main` function (or any function), and you only want to **exit the `switch`**, not the function? That’s where the **`break` statement** comes in. The `break` keyword tells the compiler: *“We’re done with the `switch`; continue with whatever comes after it.”* In other words, `break` exits just the `switch` block, allowing the function to continue running any remaining code afterward.

Here's the above program modified with `break` instead:
```cpp
// ...
void printSomething(int x) {
  switch (x) {
    case 1:
      std::cout << "One";
      break;
    
    case 2:
      std::cout << "Two";
      break;
    
    case 3:
      std::cout << "Three";
      break;
    
    default:
      std::cout << "Uknown";
      break;
  }
}
// ...
```
___
### 🔹 Fallthrough and Scoping
What would happen if we wrote a `switch` statement, but omitted any `break` or `return` statements? When execution flows from a statement underneath a label into statements underneath a subsequent label this is called **fallthrough**.

```cpp
void printSomething(int x) {
  switch (1) {
    case 1:
      std::cout << "One"; // This executes
    
    case 2:
      std::cout << "Two"; // This executes
    
    case 3:
      std::cout << "Three";// This executes
    
    default:
      std::cout << "Uknown"; // This executes
  }
}
// ...
```

Output:
```txt
OneTwoThreeUnknown%
```

This is probably not what you intended; however, if **fallthrough** is what you intend to happen, then you should be explicit about it and use the `[[fallthrough]]` attribute (C++17), followed by a semicolon (`;`).
#### Why does fallthrough happen?
You might be asking (as I asked myself):

*"Why does fallthrough happen if the case value doesn't match up with the value from the switch condition?"*

It's a reasonable question but the answer to this question helps clear up the differences between using something like an `if` statement and using something like a `switch` statement. The reason why fallthrough happens is because `switch` isn't a series of `if` statements. It does not re-check the following `case` labels after a match is found. Once a `case` matches, the program **jumps to that label** and keeps executing code **sequentially**, including through other case blocks if nothing stops it. A switch is more like a `goto` than an `if` statement (See: [[Control Flow - Jump Statements]]).
___
### 🔹 Sequential `case` Labels
If you didn't know, when writing a simple Boolean function, you can use the **logical OR** to check for multiple conditions. Example:
```cpp
bool isVowel(char c) {
  return (c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u' ||
	  c == 'A' || c == 'E' || c == 'I' || c == 'O' || c == 'U')
}
```

Similarly, and depending on your opinion, you could write it more clearly like this:
```cpp
// ...
bool isVowel(char c) {
  switch (c) {
    case 'a':
    case 'e':
    case 'i':
    // ...
      return true;
    default:
      return false;
  }
}
```
> Remember, execution begins at the first statement after a matching case label. Case labels **are not** statements (they're labels), so they don't count. This is technically considered fallthrough, but since it's idiomatic and obvious intentional, it doesn't need to be documented as such.
___
### 🧠 Flashcards

What kind of expression is allowed inside the parentheses of a `switch` statement?  
?|?  
An expression that evaluates to an **integral** or **enumerated** type.

---

What keyword exits only the `switch` block but allows the function to continue?  
?|?  
`break`

---

What keyword exits the `switch` block _and_ the enclosing function?  
?|?  
`return`

---

What happens if no `break` or `return` is used after a `case` label?  
?|?  
Execution will continue into the next `case` — this is called **fallthrough**.

---

What is the purpose of the `default` label in a `switch` statement?  
?|?  
It acts as a catch-all when no matching `case` label is found. It’s optional and typically placed last.

---

Why are `switch` statements typically limited to integral or enumerated types?  
?|?  
Because they are often implemented as jump tables, which require discrete, predictable values like integers.

---

What keyword is used in C++17 to mark intentional fallthrough?  
?|?  
`[[fallthrough]];`

---

Is it considered fallthrough if multiple `case` labels are stacked without code in between?  
?|?  
Technically yes, but it's **idiomatic and obvious**, so it doesn't require the `[[fallthrough]]` attribute.

---

Why does fallthrough happen even when the value doesn’t match the following `case` labels?  
?|?  
Because `switch` jumps to the first matching case and then continues executing **sequentially** unless told otherwise.

---

What’s the main readability benefit of using `switch` over multiple `if-else` statements?  
?|?  
It keeps code more concise and clearly shows you’re testing a single variable against multiple values.

#flashcards 