 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚8:59 pm  📆 Fri Sep 19
 🔗 **Related Concepts**: #note #cpp [[Constants & Constexpr]]
___
## 📝 Note: Compile-time Optimization
In programming, **optimization** is the process of modifying software to make it work more efficiently (e.g., to run faster or use fewer resources).

Some types of optimization are *done by hand*—a program called a **profiler** can be used to see how long various parts of the program are taking to run, and which are impacting overall performance. Other kinds of optimization tools can be performed automatically, such as **optimizer** programs that work at a low-level for ways to improve statements or expressions by rewriting, reordering, or eliminating them. Modern C++ compilers are **optimizing compilers**, meaning they are capable of automatically optimizing your programs as part of the compilation process. Just like the **preprocessor**, these optimizations do not modify your source code files; rather, they are applied transparently as part of the compilation process.

Most compilers default to no optimization, so if you use a command-line compiler like **gcc**, you'll need to enable optimization yourself, though if you work in an IDE--they will likely configure release builds to enable optimization and debug builds to disable optimization.
### 🔹 As-if Rule
In C++, compilers are given a lot of leeway to optimize programs. The **as-if rule** says that compiler can modify a program however it likes in order to produce more optimized code, so long as those modifications do not affect a program's *"observable behavior"*.

Modern compilers employ a litany of different techniques in order to optimize a program effectively. Which techniques can be applied depends on the program *and* quality of the compiler and optimizer. ***gcc** all the way! 🎉*. 
#### Some techniques used
- Loop Optimizations
- Prescient Store Optimizations
- Data-flow Optimizations
- SSA-based Optimizations
- Code Generator Optimizations
- Functional Language Optimizations
- Bounds Checking Optimizations

You don't have to know all these by heart, but as you get deeper you will start to learn about these things fundamentally.
### 🔹 Constant Folding
Consider the following program:

```cpp
#include <iostream>

int main() {
std::cout << 3 + 4 << '\n';
return 0;
}
```

One of the original forms of compile-time evaluation is called *constant folding.* **Constant folding** is an optimization technique where the compiler replaces expressions that have literal operands with the result of the expression. Using constant folding, the compiler would recognize that the expression `3 + 4` has constant operands, and then replace the expression with the result `7`.
### 🔹 Constant Propagation
The following program contains another optimization opportunity:

```cpp
#include <iostream>

int main() {

int x{7};
std::cout << x << '\n';

return 0;
}
```

When `x` is initialized, the value `7` will be stored in the memory allocated for `x`. Then on the next line, the program will go out to memoryland to fetch the value `7` so it can be printed. This requires two memory access operations.

**Constant Propagation** is an optimization technique where the compiler replaces the variables know to have constant values with their values. The result of this would be equivalent to this:
```cpp
#include <iostream>

int main() {

int x{7};
std::cout << 7 << '\n';

return 0;
}
```

This removes the need to go out and fetch `x` from memory. And in situations like this:
```cpp
#include <iostream>

int main() {

int x{7};
int y{4};
std::cout << x + y << '\n';

return 0;
}
```

We would get some constant propagations that results in constant folding, like this:
```cpp
#include <iostream>

int main() {

int x{7};
int y{4};
std::cout << 11 << '\n';

return 0;
}
```
#### Dead Code Elimination
**Dead code elimination** is an optimization technique where the compiler removes code that may be executed but has no effect on the programs behavior. Let's refer back to this last program where the program optimized with constant folding, constant propagation, and now let's see how dead code elimination optimizes:

```cpp
#include <iostream>

int main() {

std::cout << 11 << '\n';

return 0;
}
```
> 😂
### 🔹 Insights
- Using `const` and `constexpr` variables can help optimize more effectively, see: [[Constants & Constexpr]].
- Optimizations *can* make programs harder to debug.
- Notable exception to the as-if rule can be learned when learning about [[Classes and Objects(STUB)]].
___
### 📌 Key Definitions
**Compile-time Constant**
- A constant whose value is known at compile-time:
	- Literals
	- Constant objects whose initializers are compile-time constants
**Runtime Constant**
- A constant whose value is determined in a runtime context:
	- Constant function parameters
	- Constant objects whose initializers are non-constant or runtime constants.
___
### 🧠 Flashcards

**What does the “as-if rule” allow the compiler to do?**  
?|?  
Reorder, remove, or modify code **as long as observable behavior doesn’t change**.

---

**Give an example of observable behavior in C++.**  
?|?  
Input/output results, modifications of variables in memory, thrown exceptions.

---

**What is constant folding?**  
?|?  
The compiler evaluates constant expressions at compile time and replaces them with the result.

---

**What is constant propagation?**  
?|?  
Replacing variables that hold known constant values with those values directly.

---

**How can constant propagation lead to constant folding?**  
?|?  
Once constants are substituted, resulting expressions can be folded into single literal values.

---

**What is dead code elimination?**  
?|?  
The compiler removes code that doesn’t affect observable behavior.

---

**Why is `constexpr` more optimization-friendly than `const`?**  
?|?  
Because `constexpr` guarantees compile-time evaluation, allowing more folding/propagation.

---

**Why are compiler optimizations usually disabled in debug builds?**  
?|?  
Optimizations make debugging harder by changing structure, removing variables, or reordering instructions.

---

**When using gcc, how are optimizations enabled?**  
?|?  
By passing optimization flags like `-O1`, `-O2`, or `-O3` at compile time.

---

**What’s the key difference between a compile-time constant and a runtime constant?**  
?|?

- Compile-time: value known during compilation (literals, `constexpr`).
- Runtime: value fixed but only determined at runtime (e.g., const function parameters).

#flashcards 