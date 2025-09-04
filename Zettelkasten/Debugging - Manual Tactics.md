 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚5:41 pm  📆 Tue Sep 2
 🔗 **Related Concepts**: #note #cpp [[Plog]] [[Multi-File Programs]] [[Designing a Program]]
___
## 📝 Note: Debugging - Manual Tactics
### 🔹 Syntax and Semantic Errors
Software bugs and errors are impossible to avoid. No matter how skilled you are, as long as you’re human, you will make mistakes. With that in mind, rather than trying to write error-free code (which we *should* generally strive for), we should focus on learning how to debug effectively.

In this section, we'll talk about the types of errors and debugging problems you’ll encounter — and how to start building practical debugging habits into your everyday code.
___
### 🔹 Syntax Errrors
A **syntax error** occurs when you write code that violates the grammatical rules of C++. These errors prevent the program from compiling at all.
##### Common syntax errors include:
1. Missing or misplaced semicolons  
2. Mismatched parentheses or braces  
3. Strings missing opening or closing quotes  
4. Misspelled keywords (e.g., `retrun` instead of `return`)  
5. Incorrect use of operators (e.g., `= =` instead of `==`)

Fortunately, the **compiler always catches syntax errors** — and it’s rarely polite about it.
___
### 🔹 Semantic Errors
A **semantic error** is an error in *meaning*. The code is usually syntactically valid and compiles, but it doesn’t do what you intended.
Semantic errors come in two forms:
####  Compile-time semantic errors  
These violate the **rules of the language** (e.g., type mismatches, invalid conversions). The compiler catches them — but they’re not syntax errors.

**For Example:**
```cpp
#include <iostream>

int main() {
    std::cout << "Hello";
    return "Hello";
}
```
> This is a **compile-time semantic error**: it violates type rules, even though the syntax is correct.

---

#### Run-time semantic errors  
These are more subtle. The program compiles, but your **logic is wrong**.

**For Example:**
```cpp
#include <iostream>

int main() {
    int numbers[3] = {1, 2, 3};
    std::cout << numbers[5] << '\n';  // ❌ Out-of-bounds access
    return 0;
}
```
> This code compiles just fine — no syntax errors, no type mismatches.  
> But at run-time, you’re accessing an element **outside the bounds of the array**.

**Other examples include:**
- Infinite loops you didn’t mean to write  
- Dividing by zero  
- Accessing memory out of bounds  
- Any situation that leads to **undefined behavior**  

These are often the **hardest bugs to catch**, because the compiler won’t complain — but your program may crash, hang, or behave unpredictably.
___
### 🔹 Debugging Tactics
Bugs are inevitable, and debugging is a skill you’ll build over time. In small programs, you can often find issues through code inspection and intuition. But in larger or more unpredictable programs, you’ll need to **reproduce the issue**, observe the program’s behavior, and isolate the cause.

That’s where real debugging techniques come in.
___
#### 1. Commenting Out Code
If you're testing for bugs but want to reduce noise, try commenting out parts of your code to narrow down where the issue might be. This is a solid first step — especially for beginners — but it can get messy fast. You're often stuck toggling large blocks on and off, and it’s easy to forget to restore something you temporarily removed.
#####  Tip
Instead of constantly commenting/uncommenting debug code, consider using a header-only library like [`dbg`](https://github.com/sharkdp/dbg). It lets you leave debug statements in your code that get compiled out automatically in release builds via preprocessor macros.

```cpp
#include "dbg.h"

int main() {
    int value = 42;
    dbg(value); // prints the value and location, only in debug mode
}
```
It's clean, non-destructive, and great for logging quick insights without editing or removing them later.
___
#### 2. Validating Code Flow and Printing values
When debugging, use `std::cerr` instead of `std::cout` for flag messages like:

```cpp
std::cerr << "Checkpoint: about to crash\n";
```

Some tutorials suggest using `std::cerr` for debugging, even before teaching what makes it different. That can be confusing, because in simple programs, `std::cout` works exactly the same.

Here's the simple truth:
- `std::cerr` is unbuffered — it's guaranteed to print immediately, even if your program crashes.
- `std::cout` is buffered — so debug messages might get stuck and never appear.

For now, just remember:  
> **Use `std::cerr` for quick trial-and-error debugging** (e.g., checking variables or control flow). It won’t hurt, and later you’ll see why it’s actually the better tool for debugging output.
___
#### 3. Conditionalizing debug code
Consider a program where you have written a few debug statements. Before moving on, you'll need to remove all of those, or comment them out. If you want to come back and re-check, you are doing that all over again. We can mitigate this by using some preprocessor conditional logic.

**For Example**:
 
```cpp
#include <iostream>

#define ENABLE_DEBUG // comment out to disable debugging

int getUserInput()
{
#ifdef ENABLE_DEBUG
std::cerr << "getUserInput() called\n";
#endif
	std::cout << "Enter a number: ";
	int x{};
	std::cin >> x;
	return x;
}

int main()
{
#ifdef ENABLE_DEBUG
std::cerr << "main() called\n";
#endif
    int x{ getUserInput() };
    std::cout << "You entered: " << x << '\n';

    return 0;
}
```
Now we can enable debugging simply by commenting / uncommenting #define `ENABLE_DEBUG`.

#### 4. Using a logger
A **log** is sequential record of events that have happened, usually time-stamped. The process of generating a log is called **logging**. Typically logs are written to a file on disk (called a **log file**) so they can be reviewed later.
#####  `std::clog`
C++ contains an output stream named `std::clog` that is intended to be used for logging, however by default, it writes to the standard error stream just like `std::cerr` , and while its possible tor redirect it to file, it is much easier to use one of the many third-party loggers.

#####  `plog`
For illustrative purposed, lets use `plog` as an example. Plog is great because its implemented as just a set of header files, so it's easy to include anywhere you need it.
```cpp
#include <plog/Log.h> // Step 1: include the logger headers
#include <plog/Initializers/RollingFileInitializer.h>
#include <iostream>

int getUserInput()
{
	PLOGD << "getUserInput() called"; // PLOGD is defined by the plog library

	std::cout << "Enter a number: ";
	int x{};
	std::cin >> x;
	return x;
}

int main()
{
	plog::init(plog::debug, "Logfile.txt"); // Step 2: initialize the logger

	PLOGD << "main() called"; // Step 3: Output to the log as if you were writing to the console

	int x{ getUserInput() };
	std::cout << "You entered: " << x << '\n';

	return 0;
}
```

See: [[Plog]] for a detailed instructions on set up.