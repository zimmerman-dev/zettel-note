#### 📝 Note: C-Style Strings 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚9:18 pm  📆 Wed Aug 6
 🔗 **Related Concepts**: #note #cpp [[cstdlib]] , [[string]] , [[C++ Headers Index]] , [[cstring]] , [[cctype]] , [[Data Types]] , [[Arrays]] , [[Iostream]] 
___
## 🧠 Overview

C-style strings are arrays of characters (`char[]`) terminated by a **null character** (`'\0'`).  
They are low-level and require manual memory handling and caution when used.  
Common use cases include:

- Legacy C libraries
- Embedded programming
- Low-level performance-critical code

---
### 🌀 String Literals and Memory Layout

A **string literal** is what we've been using in most `std::cout` statements—it's a constant sequence of characters in double quotes, e.g., `"C++ is fun!"`.

- String literals are **immutable**
- They are **null-terminated**
- Stored as arrays of characters in memory

```cpp
char myName[] {"John Bishop"};
```
Visual layout in memory:

|  0  |  1  |  2  |  3  |  4  |  5  |  6  |  7  |  8  |  9  | 10  |  11  |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :--: |
|  J  |  o  |  h  |  n  |     |  B  |  i  |  s  |  h  |  o  |  p  | `\0` |

- This string has 11 characters.
- The compiler automatically allocates **12 bytes** to store the null terminator (`'\0'`).
- Indexing works like arrays: `'J'` is at `myName[0]`, `'o'` at `myName[1]`, etc.

### ⚠️ Pitfalls of Static Allocation

C-style strings are arrays, so they inherit the **static nature** of arrays: fixed size at compile time.

```cpp
char myName[8] {"Frank"};
myName[5] = 'y'; // OK — space was allocated
```

|0|1|2|3|4|5|6|7|
|---|---|---|---|---|---|---|---|
|F|r|a|n|k|y|`\0`|`\0`|
- The array size is 8, but `"Frank"` only uses 5 characters + 1 `'\0'`
- Two unused slots (`myName[5]`, `myName[6]`, etc.) are safely writable

 🔹 The null terminator acts as a **sentinel**, signaling the end of the string when functions like `strlen()` walk through it.

---
### 📚 `<cstring>` — String Manipulation Functions

These functions work directly on C-style strings (`char*` or `char[]`):


|         Function         |                  Purpose                  |
| :----------------------: | :---------------------------------------: |
|        `strlen()`        |   Get **length** of string (up to `\0`)   |
| `strcpy()` / `strncpy()` |        Copy one string to another         |
| `strcat()` / `strncat()` |       Append one string to another        |
| `strcmp()` / `strncmp()` |              Compare strings              |
| `strchr()` / `strrchar`  |         Find character in string          |
|        `strstr()`        |              Find substring               |
| `memcpy()` / `memmove()` | Raw memory copy (often used with `char*`) |
##### ⚠️ Watch for buffer overflows. These functions assume you know how much space you're working with.

---

### 🔡 `<cctype>` — Character Inspection Functions

These are used for checking or transforming individual `char` values:

| Function                    | Purpose          |
| --------------------------- | ---------------- |
| `isalpha(c)`                | Is alphabetic?   |
| `isdigit(c)`                | Is digit?        |
| `isalnum(c)`                | Is alphanumeric? |
| `isspace(c)`                | Is space or tab? |
| `ispunct(c)`                | Is punctuation?  |
| `toupper(c)` / `tolower(c)` | Change case      |
##### 👍 Often used when parsing input character-by-character.

---

### 🎲 `<cstdlib>` — String Conversion Functions

These functions convert `char*` → numeric types (and vice versa in some cases):


| Function               | Purpose                          |
| ---------------------- | -------------------------------- |
| `atoi(const char*)`    | Convert string to `int`          |
| `atof(const char*)`    | Convert string to `double`       |
| `strtol()`             | Safer, flexible string → `long`  |
| `strtoul()`            | Unsigned version                 |
| `strod()` / `strtof()` | Convert to `double` / `float`    |
| `getenv(const char*)`  | Get environment variable by name |
| `system(const char*)`  | Run shell command from string    |
##### 🚫 `atoi()` and friends do no error checking—prefer `strtol()` where possible.

---

### 🧵 Tips & Common Pitfalls

- Always ensure space for the **null terminator** when creating `char[]` manually.
- Use `std::string` when possible, but understand these tools for interop and legacy code.
- Mixing `std::string` with `char*`? Use `.c_str()` to convert safely.

```cpp
std::string name = "hello";
const char* raw = name.c_str();
```


### ✅ See Also

- [[string]]
- [[cstdlib]]
- [[cstring]]
- [[cctype]]

