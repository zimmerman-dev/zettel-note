 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚12:09 pm  📆 Sat Sep 20
 🔗 **Related Concepts**: #note #cpp [[string]] , [[string_view]] , [[C-Style Strings]] , [[Text & Stream Manipulation]]
___
## 📝 Note: String Syntax Reference
📎 See main conceptual note: [[string]]
### 🔹 Declaring & Initializing Strings

```cpp
#include <string>

std::string s1;             // Empty string
std::string s2 {"John"};    // Literal init
std::string s3 {s2};        // Copy init (separate memory)
std::string s4 {"John", 3}; // "Joh" (first 3 chars)
std::string s5 {s3, 0, 2};  // "Jo" (from s3 at index 0, length 2)
std::string s6 (3, 'X');    // "XXX" (repeated char)
```
___
### 🔹 String Concatenation
✅ **Legal:**
```cpp
std::string sentence = part1 + " " + part2 + " language";
```

🛑 **Illegal:**
```cpp
sentence = "C++" + " is powerful"; // C-style literals can't be added
```
___
### 🔹 Character Access: `[]` and `.at()`
```cpp
std::string name {"John"};

std::cout << name[1];     // o
std::cout << name.at(0);  // J
```
___
### 🔹 Range-Based For Loop
```cpp
for (char c : name) {
    std::cout << c;
}
```
___
### 🔹 Comparing Strings
Operators: `==`, `!=`, `<`, `>`, `<=`, `>=`

- Compared character-by-character using ASCII values
- Can compare:
  - Two `std::string` objects
  - `std::string` and C-style literals
  - `std::string` and `const char*` variables
___
### 🔹 Substrings – `.substr()`
```cpp
std::string s1 {"This is a test"};

s1.substr(0, 4);   // "This"
s1.substr(5, 2);   // "is"
s1.substr(10, 4);  // "test"
```
- First argument: **start index**
- Second argument: **number of characters**
### 🔹 Erasing & Clearing – `.erase()`, `.clear()`
```cpp
s1.erase(0, 5);  // "is a test"
s1.clear();      // ""
```
### 🔹 String Length – `.length()` / `.size()`
```cpp
std::string s1 {"John"};
s1.length();  // 4
```
- `.length()` and `.size()` are equivalent
- Returns number of visible characters (not including null terminator)
### 🔹 Searching – `.find()`
```cpp
std::string s1 {"This is a test"};

s1.find("This");   // 0
s1.find("is");     // 2
s1.find("test");   // 10
s1.find("pizza");  // std::string::npos
```
- Returns index of match or `std::string::npos` if not found
- Optional second arg: start index  
  `s1.find("is", 3);`

Pattern:
```cpp
if (s1.find("pizza") == std::string::npos) {
    std::cout << "Not found!\n";
}
```
### 🔹 Emptiness Check – `.empty()`
```cpp
std::string s1 {""};
if (s1.empty()) {
    std::cout << "String is empty.";
}
```



























___
### 📌 Key Definitions










___
### 🧠 Flashcards

