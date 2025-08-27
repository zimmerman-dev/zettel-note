♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:22 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #note #cpp [[C++ Syntax Reference]], [[Variables and Objects]], [[Type Casting]]
___
## 📝 Note: Iostream
### The Input/Output Library
The **IO library** is part of the **C++ Standard Library** and handles **basic input and output**.  
In short, it lets your programs:  
- **Get input** from the keyboard  
- **Send output** to the console, files, databases, etc.
### Including the IO Library
To use this functionality, we **include a header file** at the top of our code. We’ll cover **preprocessor directives** later, but for now, just remember the syntax:  

```cpp
#include <iostream>

//    ⬆️ Include header files here
//    ⬇️ Write your main program below

int main() {
    // program body
    return 0;
}
```
> **Remember**: header files always go **above** `main()`.

---
### 💨 `std::cout`
Once we include `<iostream>`, we gain access to an object called **`std::cout`**, which sends data to the console.  
Think of `cout` as “**character output**.”

```cpp
#include <iostream> // For std::cout

int main() {
    std::cout << "Hello, World!";  // Prints Hello, World!
    return 0;
}
```

Here, we used `std::cout` with the **insertion operator** `<<` to send data to the console.  
You can chain multiple values together using `<<`:
```cpp
std::cout << "Hello, " << "World!\\n";
```
> `\\n` is an **escape sequence** that moves the output to a new line.
---
### ⏬ `std::endl` vs. `\\n`
There are two ways to create a new line:
- `\\n` → Adds a new line.
- `std::endl` → Adds a new line **and** forces the buffer to **flush** (send everything immediately).
```cpp
std::cout << "Hello!" << std::endl; // New line + flush
std::cout << "World!\\n";            // Just new line
```
> Best practice: **prefer `\\n`** unless you specifically need to flush the buffer.
---

### 🚽 Buffering Explained *(optional)*
When you use `std::cout`, your output isn’t always sent to the console right away.  
It’s **buffered** — stored temporarily in memory and sent later in batches for efficiency.  

Think of it like a **train station**:  
- People (output) line up in the station (buffer).  
- Once the train fills up or it’s time to leave, everyone goes to the console.  
- If your program crashes before the train leaves, anything still waiting in the buffer is lost.
---
### ⌨️ `std::cin`
`std::cin` (short for **character input**) is another predefined object from `<iostream>` that lets you **read input from the keyboard**.  
We use the **extraction operator** `>>` to store user input into variables:

```cpp
#include <iostream>  // For std::cin and std::cout

int main() {
    std::cout << "Enter a number: ";
    int x{};
    std::cin >> x;

    std::cout << "You entered " << x << '\\n';
    return 0;
}
```

Just like `std::cout`, you can chain multiple extractions:
```cpp
std::cout << "Enter two numbers: ";
int a{}, b{};
std::cin >> a >> b;
std::cout << "You entered " << a << " and " << b << '\\n';
```
---
### 🧩 Key Takeaways
1. Include `<iostream>` whenever you need keyboard input or console output.  
2. `std::cout` uses the **insertion operator** `<<` to send data out.  
3. `std::cin` uses the **extraction operator** `>>` to read data in.  
4. Use `\\n` for most line breaks; use `std::endl` only if you need to **flush the buffer**.  
5. Output is **buffered** for efficiency, so not everything happens instantly.

---
### 📌 Key Definitions
- **Header File** → A file containing declarations (functions, objects, classes, etc.) that can be reused across programs using `#include`.
- **Insertion (`<<`) & Extraction (`>>`) Operators** → Special operators used with streams like `std::cout` and `std::cin` to send data out or pull data in.
- **Buffer** → A reserved area in memory where I/O data temporarily waits before being sent to its destination (console, file, etc.).
- **Preprocessor** → A program that processes source code before compilation, handling directives like `#include` and `#define`.
---
### 🧠 Flashcards

- Why is `std::endl` considered less efficient than `'\n'`?|||Because `std::endl` **flushes the output buffer** every time it’s used, which is an expensive operation, while `'\n'` just inserts a newline without flushing. #flashcards
<!--SR:!2025-08-30,4,270-->

- The `<<` operator used with `std::cout` is called the ==insertion== operator because it sends data into an output stream. #flashcards
<!--SR:!2025-08-30,4,270--> 

- What actually happens if your program crashes before the output buffer is flushed?|||Any data still sitting in the buffer is **lost** and never reaches the console (or file, DB, etc.). #flashcards
<!--SR:!2025-08-30,4,270-->

- `std::cin` uses the ==extraction== operator to take data from the user and place it into a variable. #flashcards
<!--SR:!2025-08-30,4,270--> 

- Why does the program need `#include <iostream>` before using `std::cout` or `std::cin`?|||Because `iostream` is a **header file** that **declares** these objects and related functionality. Without it, the compiler doesn’t know they exist. #flashcards
<!--SR:!2025-08-30,4,270-->

