 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚6:09 pm  📆 Wed Oct 8
 🔗 **Related Concepts**: #note #cpp [[Control Flow - Conditional Statements Overview]] , [[Control Flow - Jump Statements]] , [[Control Flow - Function Calls]] , [[Control Flow - Loops Overview]] , [[Control Flow - Halts]] , [[Control Flow - Exceptions (stub)]]
___
## 📝 Note: Control Flow - Overview
When a program is run, the CPU begins execution at the top of `main()` executes some number of statements (in sequential order by default), and then the program terminates at the end of `main()`. The sequence in which a program runs is what's known as the **execution path** (or **path** for short).
```cpp
#include <iostream>

int main() {                                   // Path begins
  std::cout << "Enter a num: ";                // 1
  
  int num{};                                   // 2
  std::cin >> num;                             // 3
  
  std::cout << "You entered " << num << '\n';  // 4
  
  return 0;                                    // Path ends
}
```
The execution path for this program is lines 4, 6, 7, 9, and 11 in that order. You'll notice that this program runs in a sort of straight line from start to finish, which is why programs like this are referred to as **straight-line programs**.
___
### Control Flow Directory
Consider our program above. What would happen if the user entered a character instead of a number? Very often, the programs we write will very rarely run from start to finish with no  derivations in the execution path. **Control Flow Statements** are statements that allow the programmer to change the normal path of execution through the program. Control flow, is what gives you the tools to solve extra complex problems.

Below are a list of notes with specific information to how control flow works in C++.

1. [[Control Flow - Conditional Statements Overview]] - Causes a sequence of code to execute only some condition(s) are met. (`if`, `else`, and `switch`).
2. [[Control Flow - Jump Statements]] - Tells the CPU to start executing the statements at some other location. (`goto`, `break`, `continue`).
3. [[Control Flow - Function Calls]] - Jump to some other location and back. (function calls, `return`)
4. [[Control Flow - Loops Overview]] - Repeatedly execute some sequence of code zero or more times, unit some condition is met. (`while`, `do-while`, `for`, `for-ranged`).
5. [[Control Flow - Halts]] - Terminate the program. (`std::exit()`, `std::abort()`).
6. [[Control Flow - Exceptions (stub)]] - A special kind of flow control structure designed for error handling. (`try`, `throw`, `catch`).

All of these will be covered in detail in their respective notes, though exceptions won't come until later. If the link still says "stub", it hasn't been finished yet.