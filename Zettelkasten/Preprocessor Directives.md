 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚6:21 pm  📆 Sun Aug 31
 🔗 **Related Concepts**: #note #cpp  [[Functions - Built-in]] , [[Iostream]] , [[C++ Syntax Reference]] , [[Constants]] 
___
###  🔹 What is the Preprocessor?
The **preprocessor** runs _before_ compilation. It prepares your source code by performing a series of **text transformations**.
#### What it does:
- Strips blank lines (not all whitespace)
- Removes comments (`//` and `/* ... */`)
- Ensures the file ends with a newline
- Processes `#` directives like `#include`, `#define`, `#ifdef`, etc.

>These changes happen **in-memory or via temp files**—your actual `.cpp` source isn't modified.
> ---
###  🔹 Translation Unit
Once preprocessing is complete, you get a **translation unit**:
> A single `.cpp` file + all its headers (recursively `#included`) + all macro expansions.

This translation unit is what the **compiler** then compiles.
> Related fact: The full process of preprocessing → compiling → linking is called **translation** (as in “translating to machine code”).
---
###  🔹 Preprocessor Directives
These start with `#` and end with a **newline** (not a semicolon). They are instructions to the **preprocessor**, not the compiler.
####  `#include`
Replaces the directive with the full contents of the included file.
```cpp
#include <iostream>   // standard library
#include "math.h"     // user-defined
```

>- `<>` → searches system paths
>- `""` → searches local directory first 

```cpp
#include <iostream>

int main() {
    std::cout << "Hello, world!\n";
    return 0;
}
```

>When this is preprocessed, the contents of `<iostream>` are inserted _in place_ before anything else happens.

We'll explore `#include` more in [[Header Files]].
___
### 🔹 Macro Defines
The `#define` directive can be used to create a macro. In C++, a **macro** is a rule that defines how input text is converted into replacement output text.
#### object-like & function-like macros
The two basic types of macros are *object and function-like* macros. **Function-like** macros act like functions, and serve a similar purpose. Their use is generally considered unsafe, and almost anything they can do can be done by a normal function. On the other hand, *object-like* macros can be defined in one of two ways.
- `#define INDENTIFIER substitution_text` 
When the preprocessor encounters this directive, an association is made between the macro identifier and the *substitution_text*. Put simply, the compiler doesn't see the identifier--it sees the substitution_text. To put even more simply, this macro is used to assign a name to a literal. **Use cautiously.**
- `#define IDENTIFIER`
This might seem pretty useless, and it _is useless_ for doing text substitution. Before we talk about object-like macros with no sub-text, lets consider a few **conditional compilation** preprocessor directives and we will bring it all the way home.
#### Conditional Compilation Directives
The conditional compilation preprocessor directives allow you to specify under what conditions something will or won't compile. First consider this program:
```cpp
#include <iostream>
#define PRINT_NAME

int main() {

	#ifdef PRINT_NAME
		std::cout << "John!\n";  // will compile since PRINT_NAME is defined
	#endif

	#ifndef PRINT_NAME
		std::cout << "John!\n";  // will not compile this code since PRINT_NAME is defined.
	#endif
	
	return 0;
}
```
##### `#ifdef` / `#if defined()`  & `#endif`
The `#ifdef`, or `#if defined()` preprocessor directive allows the preprocessor to check whether an identifier has been previously defined via `#define`. If so, whatever in-between `#ifdef` and `#endif` will be compiled. If the the identifier after `#ifdef` doesn't match up with a `#define` directive, the code does not get compiled.
##### `#ifndef` / `#if !defined()`
The `#ifndef` preprocessor directive, is the exact opposite of `#ifdef`.
##### `#if 0` & `#if 1`
Like comments, `#if 0` can be used to hide a block of code from being compiled.
```cpp
#if 0
	std::cout << "Hello!"; // This code will not compile
#endif
```
---
### 🧠 Flashcards

**Q:** What does the preprocessor produce before compilation begins?
?|?
**A:** A _translation unit_—the source file plus all included headers and macro expansions.
<!--SR:!2025-09-05,4,270-->

**Q:** What’s the difference between `#define IDENTIFIER` and `#define IDENTIFIER substitution_text`?
?|?
**A:** The first defines a macro with no replacement text (used for conditional compilation). The second defines a macro with a literal/text replacement.
<!--SR:!2025-09-02,1,230-->

**Q:** Why is `#define` still used in modern C++, despite the existence of `const` and `constexpr`?
?|?
**A:** Because `#define` enables conditional compilation via `#ifdef`, `#ifndef`, and related directives—something variables can't do.
<!--SR:!2025-09-02,1,230-->

**Q:** What is a safe, modern alternative to `#define PI 3.14` in C++?
?|?
**A:** `constexpr double PI = 3.14;`
<!--SR:!2025-09-02,1,230-->

**Q:** What kind of code structure allows you to include a header file multiple times without redefinition errors?
?|?
**A:** Header guards using `#ifndef` / `#define` / `#endif`, or `#pragma once`.
<!--SR:!2025-09-02,1,230-->

#flashcards 