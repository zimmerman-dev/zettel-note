 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚12:09 pm  📆 Mon Sep 1
 🔗 **Related Concepts**: #note #cpp [[C-Style Strings]] [[string]] [[Iostream]] 
___
## 📝 Note: Text & Stream Manipulation
##  `<cctype>` & `(ctype.h)`
This header declares a set of functions to classify and transform individual characters.
#### 🔹 **Character Classification**
These check what kind of character you’re dealing with:
- `std::isalnum(c)` → checks if `c` is alphanumeric (letter or digit) 
- `std::isalpha(c)` → checks if `c` is alphabetic
- `std::isdigit(c)` → checks if `c` is a digit (`0–9`)
- `std::islower(c)` → checks if `c` is lowercase
- `std::isupper(c)` → checks if `c` is uppercase
- `std::isspace(c)` → checks if `c` is whitespace (`' '`, `\n`, `\t`, etc.)
- `std::ispunct(c)` → checks if `c` is punctuation (`! , . ;` etc.)
#### 🔹 **Character Conversion**
These transform characters:
- `std::tolower(c)` → converts `c` to lowercase
- `std::toupper(c)` → converts `c` to uppercase
### 🔹 **Other Useful Ones**
- `std::iscntrl(c)` → checks if `c` is a control character (non-printable)
- `std::isprint(c)` → checks if `c` is printable (including space)
- `std::isgraph(c)` → checks if `c` is any printable character except space
- `std::isxdigit(c)` → checks if `c` is a valid hexadecimal digit (`0–9, A–F, a–f`)
## ✅ **Example Usage**
```cpp
#include <iostream> 
#include <cctype>  

int main() {     
	char ch {'A'};      
	
	if (std::isalpha(ch))
		std::cout << ch << " is a letter\n";
std::cout << "Lowercase: " << static_cast<char>(std::tolower(ch)) << std::endl;
}
```

You’ll often use `<cctype>` functions when:
- Validating input (checking if a character is a digit, letter, etc.)
- Normalizing strings (converting to lowercase, stripping whitespace, etc.)
- Implementing parsing logic (like checking punctuation, spaces, etc.)

These functions are **the building blocks** for a lot of string manipulation.
___
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
### 📌 Key Definitions










---
### 🧠 Flashcards

