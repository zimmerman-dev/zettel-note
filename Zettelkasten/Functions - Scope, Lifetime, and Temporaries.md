 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚11:00 pm  📆 Mon Aug 11
 🔗 **Related Concepts**: #note #cpp [[Functions - Overview]] , [[Variables and Objects]]
___
### ## 📝 Note: Functions - Scope, Lifetimes, and Temporaries
### Local Variables
 Variables defined within the body of a function are called **local variables**. Function parameters are generally considered to be local as well.  
### Local Variable Lifetime
- When a variable is defined (e.g. `int x;`), it is **instantiated** — meaning memory is allocated — when that statement is executed.
- Function parameters are instantiated and initialized **when the function is entered**.
- Variables inside the function body are instantiated at the **point of definition**, not at the start of the function.

> “An object’s **lifetime** is defined as the time between its creation and destruction.”
### 🌀 LIFO (Last-In, First-Out) Lifetime Rule
When variables go out of scope (such as at the end of a function or block), they are destroyed in the **reverse order** they were instantiated.

```cpp

#include <iostream>

void doSomething() {
std::cout << "Hello!\n";
}

int main() {
int x{ 0 }; // x's lifetime begins here

doSomething(); // x is still alive during this function call
return 0;
} // x's lifetime ends here
```

When an object is destroyed, its memory becomes invalid and it can no longer be used.
### 🔭 Scope
#### 🔬 Local Scope (a.k.a. Block Scope)
An identifier’s **scope** determines where the identifier can be seen and used within the source code.
- If an identifier is **in scope**, it can be referenced.
- If it is **out of scope**, it cannot be referenced.

The identifier of a local variable has **block scope**, meaning:
- It is usable from the point of its definition to the end of the innermost pair of `{}` braces containing it.
- For **function parameters**, the scope lasts from the start of the function body to the end of the function.

```cpp
int add(int x, int y) {  // Function parameters x and y are local variables
	int z{x + y};        // z is a local variable
	return z;
}
```

Local variable identifiers have **local scope** — they are accessible from their point of definition to the end of the **innermost** set of `{}` braces (the block).  For function parameters, their scope extends through the entire body of the function.

> Scope is a **compile-time property**, and trying to use an identifier that is not in scope will result in a compile-time error.
> ___
#### ⛔ Out-of-scope vs. "Going Out of Scope"
- **Out of scope**  
Means a variable or identifier **cannot be accessed** from the current location in the code.
- **"Going out of scope"**
Refers to the **moment** when a variable’s lifetime ends — typically at the closing brace of the block in which it was declared. This term is more commonly applied to **objects**, especially those with destructors.

```cpp
#include <iostream>

int add(int x, int y) {          // x and y enter scope (parameters)
    return x + y;                // x and y are accessible here
}                                // x and y go out of scope

int main() {
    int a {5};                   // a enters scope
    int b {2};                   // b enters scope

    std::cout << add(a, b);      // a and b are passed as arguments
    return 0;
}                                // b and a go out of scope
```
>You could rename `a` and `b` to `x` and `y`, and the program would still run correctly — because **each set of variables exists in its own scope**. Their names don’t conflict.

### 🧪 Temporary Objects
- A **temporary object** (aka **anonymous object**) is an unnamed object created by the compiler to hold a value **briefly**.
- Temporary objects have **no identifier**, **no scope**, and are destroyed **at the end of the full expression** in which they are created.
**Example:**
```cpp

#include <iostream>

int getValueFromUser() {

std::cout << "Enter an integer: ";

int input{};
std::cin >> input;

return input; // returns the value of input back to the caller
}

int main() {

std::cout << getValueFromUser() << '\n'; // where is the returned value stored?
return 0;

}
```
In the above program:
- The function returns a **copy** of the value stored in `input`.
- The caller (in `main`) receives that copy, but since it’s not stored in a named variable, it becomes a **temporary object**.
- This temporary object is then passed directly into `std::cout`.
- It is destroyed **immediately after the full expression ends** — in this case, after the `<< '\n'` operation.

See: [[Functions - Prototypes]]
___
### 📌 Key Definitions










---
### 🧠 Flashcards

**Q:** What is a local variable in C++? |?| **A:** A variable defined within a function body; it has block scope and is created at the point of definition.


**Q:** When are function parameters instantiated? |?| **A:** At the moment the function is entered; they are initialized with the caller's arguments.

**Q:** What does "going out of scope" mean in C++? |?| **A:** It refers to when an object's lifetime ends — usually at the closing brace of the block it was defined in.

**Q:** What is the destruction order of local variables in a block? |?| **A:** They are destroyed in reverse order of their instantiation — Last-In, First-Out (LIFO).

**Q:** What is the difference between scope and lifetime? |?| **A:** Scope is a compile-time rule that defines where an identifier is visible; lifetime is a runtime duration during which the object exists.

**Q:** What is a temporary object in C++? |?| **A:** An unnamed object created by the compiler to hold a short-lived value; it is destroyed at the end of the full expression.

**Q:** Do temporary objects have scope? |?| **A:** No. They do not have identifiers or scope; only lifetime.

**Q:** What happens to a local variable when its scope ends? |?| **A:** It is destroyed and its memory becomes invalid.

**Q:** What's the best practice for declaring local variables? |?| **A:** Declare them as close as possible to their first use.

**Q:** When should you use a function parameter vs a local variable? |?| **A:** Use a parameter when the value is provided by the caller; use a local variable otherwise.

#flashcards 