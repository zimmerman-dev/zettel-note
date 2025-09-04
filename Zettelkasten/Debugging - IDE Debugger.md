 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚8:01 pm  📆 Tue Sep 2
 🔗 **Related Concepts**: #note #cpp [[Debugging - Manual Tactics]] [[Plog]] [[Designing a Program]]
___
## 📝 Note: Debugging - IDE Debugger
A **Debugger** is a computer program that allows the programmer to control how another program executes and examine the program state while that program is running. The power of a debugger is twofold: The ability to precisely control execution of the program, and the ability to view (and modify, if desired) the program's state.
###  🔹Stepping
**Stepping** is the name for a set of related debugger features that let us execute (step through) our code statement by statement. There are a number of related *stepping* commands that we'll cover in turn. Open your IDE and paste this program into it:
```cpp
#include <iostream>

void printValue(int value)
{
    std::cout << value << '\n';
}

int main() {
    printValue(5);

    return 0;
}
```
#### Step Into
The **step into** command executes the next statement in the normal execution path of the program, and then pauses execution of the program so we can examine the program's state using the debugger. If the statement being executed contains a function call, *step into* causes the program to jump to the top of the function being called, where it will pause.

**Visual Studio** shortcut - F11
#### Step Over
Like *step into*, the **step over** command executes the next statement in the normal execution path of the program. However, whereas *step into* will enter function calls, and execute them line by line, *step over* will execute an entire function without stopping and return control you after the function has been executed.

**Visual Studio** shortcut - F10
#### Step Out
Unlike the other two stepping commands, **Step out** does not just execute the next line of code. Instead, it executes all remaining code in the function currently being executed, and then returns control to you when t function has returned.

- If you're in `main()`, Step Out runs the remainder of `main()` and then exits the program (no more stepping to do).
- If you're in a _user-defined function_, Step Out returns to the line **after** the function call.

It’s like saying:
> _“I’m done investigating here, just finish this function and get me out.”_

**Visual Studio** shortcut - Shift + F11
___
## Debugging Notes
These notes will be with Visual Studio in mind. The concepts are transferable, but the keyboard shortcuts may differ. To follow along and test these tools, paste this program into your IDE:
```cpp
#include <iostream>

int main()
{
	int x{ 1 };
	std::cout << x << ' ';

	x = x + 2;
	std::cout << x << ' ';

	x = x + 3;
	std::cout << x << ' ';

	return 0;
}
```
___
### 🔹 Run to Cursor  
Run to Cursor is a sort of **temporary breakpoint**, where it asks the debugger to resume execution until it hits the line where the cursor is. To enable it, go to a line with your cursor and either right-click → _Run to Cursor_, or press **Ctrl + F10**.
1.  The program runs at full speed until it:
    -   Reaches that line, then breaks into debug mode.
    -   Or it **exits/crashes/throws an exception** before getting there (in which case you’ll never stop on the line).

**Extra:** If you haven’t already started the debugger, you can still right-click → _Run to Cursor_. Visual Studio will:
-   Launch your program under the debugger,    
-   Ignore any preset breakpoints,    
-   And stop execution at your chosen line.    

>💡 Unlike a normal breakpoint, Run to Cursor doesn’t persist — it vanishes once you hit it.
___
### 🔹 Continue  
The **Continue** debug command (**F5** in Visual Studio) simply continues running the program as per normal, either until the program terminates, or until something triggers control to return back to you again (such as breakpoint).
-   It does **not** stop on each line.    
-   If there are no breakpoints left in the path of execution, the program will just keep running until it either:    
    -   **Finishes execution**    
    -   **Crashes**    
    -   **Throws an exception** that breaks into the debugger
        
### 🔹 Start  
Similar to **Continue**, the **Start** command performs the same action as Continue, just starting from the beginning of the program. It can only be invoked when not already in a debug session.
___
### 🔹 Breakpoints  
Breakpoints are a special marker that tells the debugger to stop execution of the program at the **breakpoint** when running in debug mode. Execution pauses **before the line executes**, so you can inspect variables first.

There are multiple ways to set breakpoints, but I have found that all graphical IDEs universally allow you to simply click in the gutter of the line you want to set a breakpoint. To remove a breakpoint, just click it again. You can also right-click → _Toggle Breakpoint_ on a statement, or press **F9** in Visual Studio.

>💡 Breakpoints only work when debugging. You can also disable them temporarily or make them _conditional_ (stop only if an expression is true).
___
### 🔹 Set Next Statement  
This command is fairly uncommon, but worth referencing all the same. The **Set Next Statement** command allows us to change the point of execution to another statement (sometimes informally called _jumping_). This lets us skip over code or re-run earlier code.
-   You can move the execution point **forward** to skip instructions.    
-   You can also move it **backward** to re-run code, but state changes (like variable modifications) are not undone.    
-   You can only jump **within the same function**.

>💡 Powerful for testing, but risky if you skip initialization or double-run cleanup code.
___

### Watching Variables
Refer to the program above. **Watching a Variable** is the process of inspecting the value of a variable while the program is executing in debug mode.

Start a debug session in Visual Studio, and either **Run to Cursor** on line 6, or step into until you reach line 6. At this moment, if you hover over `x` on line 6, it will show the value as `1`.

 If you hover over `x` on line 12, it will also show `1`. That’s because the debugger reports the **current value of the variable at the stop point**, not what it will eventually become later in the code.

>💡 In Visual Studio, you can also highlight the variable and right-click → _Quickwatch_, and a sub-window will pop up containing the current value of the variable.
___
####  The Watch Window

Using the mouse to hover is fine if you want to know the value of a variable at a particular point in time, but it’s not well-suited for watching a value change as you run the code. The **Watch Window** is where you can add variables you’d like to continually inspect, and their values will update as you step through the program.

The Watch Window is only available while debugging. If it doesn’t appear by default, go to the top menu: _Debug menu > Windows > Watch > Watch 1_.

To add a variable, you can:
-   Right-click a variable → _Add Watch_
-   Or manually type the variable’s name into the Watch Window

>💡 This makes it easy to track values across multiple lines without hovering every time.

⚠️ Caution:
- The Watch Window isn’t some magical history recorder — it just mirrors the **current state of the program at the pause point**. 
- If you add a variable to the Watch Window that goes out of scope, Visual Studio will show it as “not in scope” or “undefined.”

#### Cool Features
The Watch Window can also evaluate expressions, not just variables.

💡 Example: Set up the program for a debug session and run to cursor on line 12. In the Watch Window, enter `x+2` — it will show the result evaluates to `8`.
___
####  Watchpoints

Some debuggers, like Visual Studio, allow you to set a **breakpoint on a variable** rather than on a line of code. This is called a **watchpoint** (or _data breakpoint_ in Visual Studio). The program will stop execution whenever the value of the variable changes.

To set one:
1.  Start a debug session.    
2.  Make sure the variable is in the Watch Window.    
3.  Right-click the variable → **Break when the value changes**.
    
⚠️ Caution:
- Watchpoints don’t persist between debug sessions. You’ll need to re-enable them each time.  
- If the variable goes out of scope, the watchpoint becomes invalid.
- Setting too many watchpoints can slow debugging because the debugger has to monitor memory writes constantly.
___
#### Local Watches
Since inspecting the values of local variables inside a function is common while debugging, many debuggers will offer a quick way watch the value of **all** local variables in scope.

In Visual Studio:
You can see the value of all local variables in the *Locals* window. This can be found at _Debug menu > Windows > Locals_.
___
### 🔹 Call Stack

The **call stack** is a record of which functions have been called, and in what order, to reach the current point of execution.

The **Call Stack Window** is a debugger window that displays the current call stack, so you can see how the program reached the line it’s about to execute.

If you don’t see it in Visual Studio, it can be found via _Debug menu > Windows > Call Stack_.

Paste this program into your IDE, and without any breakpoints step into the program. Step into each line and inspect when the function is shown in the call stack:

```cpp
#include <iostream>

int foo(int x) {
    x += 1;
    return x;
}

int main() {
    int b = foo(2);
    std::cout << b;
    return 0;
}
```

The _top of the stack_ is always the currently executing function. Step through `foo(int)` and notice the order of the functions being shown. When `foo(int)` finishes, the call stack pops `foo` off, and the top is back to `main()`.

📌 A function appears in the **Call Stack** the moment execution enters it, and it disappears when that function finishes and control returns to its caller.

### 🔹Intro to unit-testing
A common way to test to your functions is write a function that tests edge cases.
For example:
```cpp
#include <iostream>

int add(int x, int y)
{
	return x + y;
}

void testadd()   // Unit test for add()
{
	std::cout << "This function should print: 2 0 0 -2\n";
	std::cout << add(1, 1) << ' ';
	std::cout << add(-1, 1) << ' ';
	std::cout << add(1, -1) << ' ';
	std::cout << add(-1, -1) << ' ';
}

int main()
{
	testadd();

	return 0;
}
```

In this example, the `testadd()` function tests `add()` by calling the function with different values. If all of our values match our expectations, then we can be reasonably confident the function works.

### 🔹 Static Analysis Tools
We are bound to make certain, common mistakes. Some of those mistakes will take some of the methods above to troubleshoot and solve. Meanwhile, so mistakes are so common that modern developments software has created tools to look for these common mistakes. These are called **Static Analysis Tools**. Also known as *linters*, these programs help analyze your source code to identify specific semantic issues. While your compiler does some light static analysis, common recommend static analysis tools include: clang-tidy, cpplint, cppcheck, SonarLint, and more. Most of these have extensions that allow them to be integrated smoothly into your IDE.

---
### 📌 Key Definitions
- **Syntax Error**: An error that occurs when you write a statement that is grammatically incorrect according to the C++ Language. The compiler will catch these.
- **Semantic Error**: An error that occurs when you write a syntactically valid statement, yet it breaks the logic of what the programmer intended.
- **Debugging**: The process of finding and removing errors in a program.
- **Static Analysis Tools**: Tools that analyze your code and look for semantic issues that may indicate problems with your code.
- **Logging / Log File**: The process of writing information to a log file. A log file is a file that records events that occur in a program.
- **Refactor**: The process of restructuring your code without changing the intended behavior.
- **Unit Testing**: A software testing method by which small units of source code are tested to determine whether they are correct.
- **Stepping**: The name of a set of related debugging features that allow you to *step through* your code statement by statement.
- **Step into**: Executes the next statement is the normal execution path and then pauses for the user to regain control. A *step into* causes the program to jump to the top of the function being called.
- **Step over**: Executes the next statement in the normal execution path, and then pauses for the user to regain control. If the statement contains a function call, *step over* executes the function and returns control after the function has been executed.
- **Step out**: Executes all remaining code in the function currently being executed and then returns control you when the function has returned.
- **Return to Cursor**: Executes the program until execution reaches the statement selected by your mouse cursor.
- **Continue**: Runs the program until the program terminates or runs into a breakpoint.
- **Breakpoint**: Is a special marker that tells the debugger to stop execution of the program when the breakpoint is reached.
- **The Call Stack**: The call stack is the list of active functions that have been executed to get to the current point of execution.
---
### 🧠 Flashcards

