 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚6:38 pm  📆 Wed Oct 8
 🔗 **Related Concepts**: #note #cpp
___
## 📝 Note: Control Flow - Halts
Lets briefly cover what it means for a program to terminate itself *naturally*. When the `main()` function returns (either by reaching the end of the function, or via a `return` statement), a number of things happen:
1. All the local variables and function parameters are destroyed.
2. A special function called `std::exit()` is called, with the return value from `main()` (the `status code`) passed in as an argument. 
 
So what is `std::exit()`?
___
### 🔹 `std::exit()`
`std::exit()` is a function that causes the program to terminate normally. What does **Normal termination** mean?
1. the program has exited in an expected way. 
2. Normal termination does not imply whether it was successful or not—that's what the `status code` is for.

For example, let's say you were writing a program where you expected the user to type in a filename to process. If the user typed in an invalid filename, your program might return a non-zero `status-code` to indicate the failure state, but would still have a **normal termination**.

`std::exit()` performs a number of cleanup functions (static and global variables).

Example:
```cpp
#include <iostream>
#include <cstdlib>

void cleanup() {
std::cout << "cleanup!\n";
}

int main() {
  std::cout << 1 << '\n';
  cleanup();
  
  std::exit(0);
  
  std::cout << 2 << '\n';
  
  return 0;
}
```

Prints:
```bash
1
cleanup!
```

Notice how the statements after `std::exit()` never execute because to program has already terminated.
___
### 🔹 `std::exit()` vs. `std::atexit()`
Because `std::exit()` terminates the program immediately, it doesn't clean up local variables. You may want to manually do some cleaning.

That’s where `std::atexit()` comes in: it lets you register custom cleanup functions to run _before_ the program fully exits. This makes using `std::exit()` more reasonable in real-world code, because you can still ensure important things happen — like logging, closing files, or saving state — even if you're exiting early.





### 📌 Key Definitions
A **halt** is a control flow statement that terminates the program. 
___
### 🧠 Flashcards
