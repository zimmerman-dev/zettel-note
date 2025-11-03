 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚6:38 pm  📆 Wed Oct 8
 🔗 **Related Concepts**: #note #cpp
___
## 📝 Note: Control Flow - Halts
Let’s briefly cover what it means for a program to terminate *naturally*. When the `main()` function returns (either by reaching the end of the function, or via a `return` statement), a number of things happen:
1. All the local variables and function parameters are destroyed.
2. A special function called `std::exit()` is called, with the return value from `main()` (the `status code`) passed in as an argument. 

This call to `std::exit()` is **performed by the C++ runtime**, not by your code. It happens only after `main()` ends normally — meaning that cleanup (like local variable destruction) has already occurred.
 
So what is `std::exit()`?
___
### 🔹 `std::exit()`
`std::exit()` is a function that causes the program to terminate normally. What does **Normal termination** mean?
1. the program has exited in an expected way. 
2. Normal termination does not imply whether it was successful or not—that's what the `status code` is for.

For example, let's say you were writing a program where you expected the user to type in a filename to process. If the user typed in an invalid filename, your program might return a non-zero `status-code` to indicate the failure state, but would still have a **normal termination**.

`std::exit()` does not clean up **local** variables on the stack (because it does not unwind the call stack — it jumps straight to shutdown), but it does:
- run any functions registered with `std::atexit()`
- destroy static and global variables (which live in global storage)

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

Notice how the statements after `std::exit()` never execute because the program has already terminated.
___
### 🔹 `return` vs `std::exit()`

| Behavior                            | `return` from `main()` | `std::exit()`        |
|-------------------------------------|-------------------------|----------------------|
| Exits the program                   | ✅ Yes                  | ✅ Yes               |
| Returns a status code to the OS     | ✅ Yes                  | ✅ Yes               |
| Destroys local variables (stack)    | ✅ Yes                  | ❌ No                |
| Runs `std::atexit()` functions      | ✅ Yes                  | ✅ Yes               |
| Destroys static/global variables    | ✅ Yes                  | ✅ Yes               |

> 💡 `return` is the clean, natural way to exit.  
> `std::exit()` is a blunt tool — useful when you need to stop *now*, but risky if you're managing resources manually.

### 🔹 `std::exit()` vs. `std::atexit()`
Because `std::exit()` terminates the program immediately, it doesn't clean up local variables. You may want to manually do some cleaning.

That’s where `std::atexit()` comes in: it lets you register custom cleanup functions to run _before_ the program fully exits. This makes using `std::exit()` more reasonable in real-world code, because you can still ensure important things happen — like logging, closing files, or saving state — even if you're exiting early.

```cpp
#include <cstdlib> // for std::exit()
#include <iostream>

void cleanup()
{
    // code here to do any kind of cleanup required
    std::cout << "cleanup!\n";
}

int main()
{
    // register cleanup() to be called automatically when std::exit() is called
    std::atexit(cleanup); // note: we use cleanup rather than cleanup() since we're not making a function call to cleanup() right now

    std::cout << 1 << '\n';

    std::exit(0); // terminate and return status code 0 to operating system

    // The following statements never execute
    std::cout << 2 << '\n';

    return 0;
}
```
___
### 📌 Key Definitions
A **halt** is a control flow statement that terminates the program. 
___
### 🧠 Flashcards

What does `return 0;` from `main()` actually do?
?|?
It ends the program normally, destroys all local variables (unwinds the stack), and passes `0` to the OS as a success status code.

___

What is the key difference between `return 0;` and `std::exit(0);` inside `main()`?
?|?
`return 0;` performs full cleanup and then exits; `std::exit(0);` skips local cleanup and jumps straight to termination.

___

Does `std::exit()` destroy local (stack) variables?
?|?
No. `std::exit()` does not unwind the call stack, so local variables are not destroyed.

___

What kind of variables or functions *are* cleaned up by `std::exit()`?
?|?
Static/global variables and any functions registered with `std::atexit()`.

___

How do you register a function to be run automatically when `std::exit()` is called?
?|?
Use `std::atexit(yourFunction);` — the function must take no parameters and return `void`.


#flashcards 