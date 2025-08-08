#### 📝 Note: Functions 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:21 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #cpp #note
___

### 🔧 Function Definition

A **function definition** provides the **actual implementation** of a function. It tells the compiler what the function **does** when it's called.

![[Function Structure.png]] 
#### It includes:

- the **return type** - The type of the data that is returned from the function.
- the **function name** - *See* [[Variables and Constants]] *for naming rules.*
- the **parameter list** - The variables passed into the function. Types must be specified. Functions don't necessarily need parameters.
- and a **body** containing the statements to execute (in curly braces).

Structure
```cpp
return_type function_name(parameter_list) {
	// Function body
}
```

### 🔁 What Does "Return" Mean?
- **(Output != Return)**

A **return value** is data that a function sends _back_ to the part of the program that called it. Think of it like this:

- Call a function → it does some work
- Then it **returns** a value to you (like an answer)
- You can then use that value in a variable, expression, or output
### ✅ Using `return` Keyword

A function that has a return type **must** use the `return` statement to provide a value of that type:

```cpp
int add(int x, int y) {
    return x + y;
}
```

###  🏷️ C++ Return Types — Overview

```cpp
returnType functionName(parameters) {
    // function body
    return value;  // (if not void)
}
```

- `int` - Returns an integer 

- `double` - Returns a floating point number

- `bool` - Returns a true or false

- `char` - Returns a single character

- `std::string` - Returns a string

- `void` - The No Return Value
In C++, void is a special return type that means a function does not return anything.

```cpp
void greet() {
	std::cout << "Hello, world!";
	return;  // Optional
}
```

You still use `return;` if you want to exit early — but **not** with a value.


### 🧠 Pro tip: Match the Return Type

If your function says it will return `int`, it must return an integer — no cheating. The compiler will throw a fit if types don’t match.


### Function core ideas










- prototype
- default parameter values
- overloading
- passing arrays to functions
- pass-by-reference
- inline functions
- auto return types
- recursive functions

### What is a function?
C++ Programs
- C++ Standard Libs
- Third party libs
- our own functions

Functions allow the modularization of a program.
 - separate code into logical self-contained units
 - these units can be reused

*Don't worry about HOW the function works internally unless you're the one writing the function.*





