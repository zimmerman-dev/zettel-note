♻️ (*MinGW, Windows11, Codelite*)   
 ⌚11:04 pm  📆 Mon Aug 11
 🔗 **Related Concepts**: #note #cpp [[Functions - Overview]] , [[Functions - Parameters & Arguments]], [[Functions - User-defined]]
___
## 📝 Note: Functions - Default Arguments
When a function is called, all arguments must be supplied—**unless** you provide **default values** for parameters ahead of time. These default values are known as **default parameter values**, and the value actually used during a function call (when the caller omits an argument) is called a **default argument**

**Default parameter** values can be written in the **prototype** or the **definition**, but **not both**. (Best practice is to put them in the prototype.)  
They must also appear **at the tail end** of the parameter list—**you can’t follow a default parameter with a non-default one.**
####  So, What’s the Difference?
A **default argument** is a value provided in a function declaration (or prototype) that is used if the caller does not supply an argument for that parameter.

- A **default parameter value** is the value assigned in the function declaration or prototype:
  ```cpp
  void greet(std::string name = "Guest"); // ← default parameter value
  ```
- A **default argument** is what the compiler inserts during a function call when no argument is provided:
  ```cpp
  greet(); // ← "Guest" is used as the default argument here
  ```

Think of it this way:  
 *You define the default parameter value once* — and  
 *It becomes a default argument each time the caller omits that argument*.

#####  Syntax
```cpp
return_type function_name(param1 = value1, param2 = value2, ...);
```
> ⚠️ Default arguments must be placed **right to left**.  
> ❌ You **cannot** have a parameter with a default followed by one without.
#####  Example
```cpp
void greet(std::string name = "Guest") {
	std::cout << "Hello, " << name << "!\n";
}

int main() {
	greet();         // Outputs Hello, Guest!  ← default argument used
	greet("Jan");    // Outputs Hello, Jan!    ← no default needed
}
```

|Call|Parameter Supplied?|Argument Used|
|---|---|---|
|`greet("Jan")`|Yes|`"Jan"`|
|`greet()`|No|`"Guest"` (default)

>[!warning] ❗ **Use in Function Prototypes** ❗
You typically place default arguments in function declarations (prototypes), not in definitions, to avoid redeclaration errors.
### 🔹 When to Use
Use default arguments and default parameter values when:
- You want to provide optional parameters.
- You want simpler function calls in most use cases.
- You want to avoid writing multiple overloaded versions of a function.
### 🔹 When **Not** to Use
Avoid default arguments if:
- They make the function's behavior hard to predict.
- You're writing code for large teams or APIs where implicit behavior could be confusing.
- You're mixing them with **function overloading**, which can cause ambiguity or unexpected matches.
---
### 🧠 Flashcards

**Q: What is a _default parameter value_?** |?| A: A value provided in the **function declaration** (or prototype) that is used if the caller does **not** supply an argument.

**Q: What is a _default argument_?** |?| A: The actual value used by the compiler when the caller omits a matching argument. It is inserted automatically based on the default parameter value.

**Q: Where should you place default parameter values — in the function definition or the prototype? Why?** |?| A: In the **prototype/declaration**, to avoid redeclaration errors. Best practice is to declare them once, in the header or at the top of the source file.

**Q: What is the rule about parameter order when using default arguments?** |?| A: **Default parameters must appear at the end** of the parameter list. You cannot follow a defaulted parameter with one that lacks a default.

**Q: Code Review — What’s wrong with this declaration?**
```cpp
void show(int x = 5, int y); 
```
?|?
**A:** ❌ Invalid — a non-default parameter (`y`) cannot follow a defaulted one (`x`).

**Q: Code Review — What will this output?**
```cpp
#include <iostream>

void greet(std::string name = "Guest");

int main() {
    greet();
    greet("Alex");
}

void greet(std::string name) {
    std::cout << "Hello, " << name << "!\n";
}
```
?|?
```cpp
Hello, Guest!  
Hello, Alex!
```
The default argument is inserted when `greet()` is called with no arguments.

#flashcards 