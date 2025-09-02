 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚7:14 am  📆 Mon Sep 1
 🔗 **Related Concepts**: #note #cpp [[Multi-File Programs]] [[Preprocessor Directives]] [[Namespaces]]
___
## 📝 Note: Header Files
Conventionally, a header file could be something like `<iostream>` or your own header file within your project file. Header files are also used to propagate a bunch of related forward declarations into a code file. 

See [[Multi-File Programs]] to see how this can be done. Here is a shortened version of what this means.
###### `add.h`
```cpp
// We really should have a header guard here, but will omit it for simplicity (we'll cover header guards in the next lesson)
// This is the content of the .h file, which is where the declarations go
int add(int x, int y); // function prototype for add.h -- don't forget the semicolon!
```

In order to use this header file in main.cpp, we have to `#include` it (using quotes, not angle brackets because the header is within our project directory).
###### `main.cpp`
```cpp
#include "add.h" // Insert contents of add.h at this point.  Note use of double quotes here.
#include <iostream>

int main()
{
    std::cout << "The sum of 3 and 4 is " << add(3, 4) << '\n';
    return 0;
}
```
###### `add.cpp`
```cpp
#include "add.h" // Insert contents of add.h at this point.  Note use of double quotes here.

int add(int x, int y)
{
    return x + y;
}
```

Here is a diagram of what happens when you build this project.
![[headerfile.png]]
### 🛡️ Header Guards
When a header file is included in **multiple translation units**, it may be processed **more than once**—which can lead to **multiple definition errors**.
####  Header Guards prevent this.
The classic pattern looks like:
```cpp
#ifndef MY_HEADER_H
#define MY_HEADER_H

// contents of your header file

#endif // MY_HEADER_H
```

This ensures that the header file is only processed **once per translation unit**, no matter how many times it's `#include`d.

> The macro name (`MY_HEADER_H`) should be unique. Convention is to UPPERCASE and use underscores.
___
#### `#pragma once`
A modern, cleaner alternative:

`#pragma once`

✅ Easier to read  
✅ Less error-prone  
❌ Not technically standard, but **widely supported**
___
### 🧠 Flashcards

