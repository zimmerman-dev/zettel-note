 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚10:37 am  📆 Sun Aug 31
 🔗 **Related Concepts**: #note #cpp [[Functions - Prototypes]] , [[Namespaces]] , [[Functions - Scope, Lifetime, and Temporaries]]
___
## 📝 Note: Multi-File Programs
### 🤔 Why split files?
As your C++ projects grow, it becomes easier to organize your logic into **multiple** `.cpp` **files**. This modular design:
- Keeps `main.cpp` clean
- Makes your code easier to debug
- Encourages reusability
### 🧱 Starting with a basic setup
Let’s say you define a function in `foo.cpp` and want to use it in `main.cpp`.
##### 🗂️ Project Tree (Basic Version)
```bash
project/
├── src/
│ ├── foo.cpp
│ └── main.cpp
```
##### 📄 foo.cpp
```cpp
#include <iostream>

int foo(int& x) {
return x += 1;
}
```
##### 📄 main.cpp
```cpp
#include <iostream>

int foo(int&); // 👈 Manual prototype

int main() {
int x{5};
foo(x);
std::cout << x;

return 0;
}
```

>This works! But...
>As you add more files, manually writing prototypes becomes error-prone and messy.
>---
### 📦 Header File Version (Scalable)
Instead of writing the prototype manually, put it in a `.h` file and `#include` it.
##### 🗂️ Project Tree (Improved Version)
```bash
project/
├── src/
│ ├── foo.cpp
│ ├── foo.h
│ └── main.cpp
```
##### 📄 foo.h
```cpp
#ifndef FOO_H
#define FOO_H

int foo(int&);

#endif // FOO_H
```
##### 📄 foo.cpp
```cpp
#include <iostream>
#include "foo.h"

int foo(int& x) {
return x += 1;
}
```
##### 📄 main.cpp
```cpp
#include <iostream>
#include "foo.h"

int main() {
int x{5};

foo(x);
std::cout << x;
return 0;
}
```

>This is safer, cleaner, and scalable.
>No more manual declarations. You can reuse `foo.h` across files.
>---
### 🛡️ Header Guards
Prevent multiple definitions:
```cpp
#ifndef FOO_H
#define FOO_H
// prototype goes here
#endif // FOO_H
```

Or use the more modern shorthand:
```cpp
#pragma once
```
### ⚔️ Naming Collisions
Header files help you avoid mistakes like:
- Redeclaring a function prototype inconsistently
- Repeating function names across files
- Polluting the global namespace
### 🧠 Recap

|         Concept         | Manual Approach | With Header File |
| :---------------------: | :-------------: | :--------------: |
| Prototype in `main.cpp` |   ✅ Required    |   ❌ Not needed   |
|       Reusability       |    ❌ Limited    |      ✅ High      |
|   Risk of collisions    |    ⚠️ Higher    |     ✅ Safer      |
|   Project scalability   |  🚫 Not ideal   |    ✅ Modular     |
### ⚙️ Compile
```bash
g++ src/main.cpp src/foo.cpp -o program
```
Later you’ll automate this with CMake, but for now, this is all you need.