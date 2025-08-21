#### 📝 Note: Functions - Scope 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚11:00 pm  📆 Mon Aug 11
 🔗 **Related Concepts**: #note #cpp [[Functions - Overview]] , [[Variables and Constants]]
___
### 🔭 Scope
#### 🔬 Local Scope (a.k.a. Block Scope)
An identifier's **scope** determines **where in the code** that identifier can be accessed.
##### 🧱 Local Variables
Variables declared inside a function (including parameters) are called **local variables**. Their scope is limited to the function or block in which they're defined.

```cpp
int add(int x, int y) {  // Function parameters x and y are local variables
	int z{x + y};        // z is a local variable
}
```
>Local variable identifiers have **local scope** — they are accessible from their point of definition to the end of the **innermost** set of `{}` braces (the block).  For function parameters, their scope extends through the entire body of the function.
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

See: [[Functions - Prototypes]]