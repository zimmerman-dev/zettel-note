 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚8:39 pm  📆 Mon Aug 25
 🔗 **Related Concepts**: #note #cpp
___
## 📝 Note: Variables and Objects
### 🔑 Key Insights
A **computer program** is a collection of instructions that manipulate data to produce a desired result. Programs themselves, whether source code or compiled executables, are also **data**. In context, we typically use **“code”** to mean the program itself. **Data** refers to the information the program works with to produce a result.

- A **data value** is a single piece of data: numbers, letters, symbols, or sequences of letters.
-  **literal** is a _hardcoded_ data value written directly in source code.   
#### Example
```cpp
std::cout << 3;    // integer literal
std::cout << 'A';  // char literal
std::cout << "A";  // string literal
std::cout << 3.0;  // double literal
std::cout << 3.0f; // float literal
```
> Literals are **read-only** data. To store or manipulate values, we need a way to put them into memory — that’s where objects and variables come in.

---
### 📦 Random Access Memory (RAM)
Random Access Memory, or **RAM**, is the computer’s main working memory. When a program runs, the **OS** loads it into RAM. Any hardcoded data (literals) in the program gets loaded at this time. The OS also reserves additional RAM for the program to use while running.  

Common uses include:
   - Storing user input.        
   - Storing data read from files, networks, or databases. 
   - Holding intermediate values calculated during program execution.

Think of RAM as a series of numbered boxes where data is temporarily stored while the program runs:
```text
[R]--[A]--[M]--[R]--[A]--[M]--[R]--[A]--[M]
|----------------------------------------->
```
> In older languages, programmers could directly access these “boxes.” In C++, we almost never do.

---
### 🍎 Objects and Variables
 In C++, **direct memory access** is discouraged. Instead, we work with **objects**, which represent regions of storage (RAM or CPU registers) that hold values.
    
- Rather than saying, _“Go get the value at mailbox 23,”_ we say,  
    _“Go get the value stored in this object,”_  
    and let the compiler figure out the location behind the scenes.
    
- Objects can be **unnamed**, but typically we assign them identifiers.  
    An object **with** a name is called a **variable**.
### Variables
A variable is an abstraction for a memory location. It allows programmers to use meaningful names and not memory addresses.

Variables must be declared before used.
```cpp
int x;     // Declaration Statement
int x, y;  // Legal declaration of multiple variables
```
- Type: integer, real number, string, etc., ...
- Value: the contents i.e. 1, 10.2, "string", etc., ...
#### Naming Standards:
 - Can contain letters, numbers, and underscores. Case sensitive.
 - Must begin with a letter or underscore (cannot begin with a number).
 - Cannot use C++ reserved keywords.
 - Cannot redeclare a name in the same scope 
#### Best Practices:
 - Be consistent with your naming conventions. 
 - Use meaningful names.
 - Never use a variable before initializing them.
 - Declare variables close to when you need them in your code.
### Initializing Variables
```cpp
int age;        // Unitialized

int age = 21;   // C-like initialization

int age (21);   // Constructor initialization

int age {21};   // C++11 list initialization syntax
```

___

### 'Global' and 'Local' Variables
- Up to this point we've declared our variables within the curly braces of the main function. This is what's known as a *local variable* because their scope or visibility is limited to statements within the main function.
- Variables declared outside of any function are called *global variables.* Unlike local variables, global variables are automatically initialized to zero.
```cpp
#include <iostream>

int x = 3;  // Global Scope

int main() {
	int x = 1; // Local Scope
	std::cout << x; // Prints 2 because it defers to the local x
	return 0;
}
```
---
### 📌 Key Definitions
- **Data**: Data is any information the can be moved, processed or stored by a computer.
- **Value**: Or **data value** is a single piece of data: numbers, letters, symbols, or sequences of letters.
-  **literal:** A _hardcoded_ data value written directly in source code.   
- **Random Access Memory**: Or **RAM** for short, is the computer’s main working memory.
- **Object**: Generally, an object refers to an unnamed *object* in memory, a variable, or a function. In C++ the term *object* has a narrower definition that excludes functions.
- **Variable**: a named object.'
- **Identifier**: The name of the variable.
- **Global Variable**: A variable visible to the the entire scope of the program because its defined outside all functions.
- **Local Variable**: Local scope is contextual the function where the variable is defined. Meaning, a variable defined inside of a function is local to the function.

---
### 🧠 Flashcards

A program is made of instructions that manipulate ==data== to produce a desired result. #flashcards
<!--SR:!2025-08-29,4,270-->

**What do we mean by “data” in programming?**|||The information the program works with to produce a result. #flashcards
<!--SR:!2025-08-28,3,250-->

A ==literal== is a hardcoded data value written directly in source code. #flashcards
<!--SR:!2025-08-29,4,270-->

**What is a value?**|||A single piece of data, such as a number, letter, symbol, or string. #flashcards
<!--SR:!2025-08-28,3,250-->

**What is a literal?**|||A hardcoded data value written directly in source code. #flashcards
<!--SR:!2025-08-29,4,270-->

**Why are literals unique kinds of data?**|||Read‑only data; they cannot be modified during program execution. #flashcards
<!--SR:!2025-08-29,4,270-->

**To store or modify data, instead of using literals directly, we use…**|||Objects and variables. #flashcards
<!--SR:!2025-08-29,4,270-->

**What is the main purpose of RAM?**|||It’s the computer’s main working memory where programs and data are loaded while running. #flashcards
<!--SR:!2025-08-28,3,250-->

**When a program starts, the OS does what with the program?**|||Loads it into RAM and reserves additional space for variables and calculations. #flashcards
<!--SR:!2025-08-29,4,270-->

**Think of RAM as…**|||A series of numbered boxes where data is temporarily stored while the program executes. #flashcards
<!--SR:!2025-08-29,4,270-->

**Name three common uses for RAM while a program runs.**|||Storing user input; holding data read from files, networks, or databases; keeping intermediate values during calculations. #flashcards
<!--SR:!2025-08-29,4,270-->

**Why don’t we usually access memory directly in C++?**|||Because we use objects to represent storage locations, letting the compiler handle memory addresses. #flashcards
<!--SR:!2025-08-26,1,230-->

**What does an object represent?**|||A region of storage (RAM or CPU register) that holds a value. #flashcards
<!--SR:!2025-08-26,1,230-->

An object with a name is called a ==variable==. #flashcards
<!--SR:!2025-08-29,4,270-->

Instead of saying “Go get the value at mailbox 23,” we say “Go get the value stored in this ==object==,” and let the compiler figure out where it lives. #flashcards
<!--SR:!2025-08-29,4,270-->aZ

**What does a variable represent in C++?**|||An abstraction for a memory location, using a meaningful name instead of an address. #flashcards
<!--SR:!2025-08-28,3,250-->

Variables must be ==declared== before they are used. #flashcards
<!--SR:!2025-08-29,4,270-->

**Give an example of declaring multiple variables at once.**|||`int x, y;` #flashcards
<!--SR:!2025-08-29,4,270-->

**What defines what kind of data a variable can store?**|||Its type, such as int, double, char, etc. #flashcards
<!--SR:!2025-08-29,4,270-->

**What is a local variable?**|||A variable declared inside a function, visible only within that function. #flashcards
<!--SR:!2025-08-29,4,270-->

**What is a global variable?**|||A variable declared outside all functions, visible to the entire program. #flashcards
<!--SR:!2025-08-29,4,270-->

If a local and global variable share the same name, the ==local== variable shadows the ==global== one. #flashcards
<!--SR:!2025-08-29,4,270!2025-08-29,4,270-->  

Global variables are automatically initialized to ==zero== if no value is given. #flashcards
<!--SR:!2025-08-29,4,270-->  