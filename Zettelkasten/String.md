#### 📝 Note: Strings
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:27 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #cpp #note [[C++ Headers Index]] ,
 [[Standard Template Library]] , [[Variables and Constants]] , [[C++ Syntax Reference]] , [[cstring]] , [[cstdlib]] , [[cctype]] , [[Boolean Logic]]
___

`std::string` is a **class** in the **Standard Template Library (STL)**.

- `#include <string>`
- Resides in the `std` namespace
- Contiguous in memory
- Dynamically sized (If C-style strings are like arrays, C++ strings are like vectors)
- Works with `iostream`
- Offers many useful member functions
- Supports familiar operators — see [[Operators]]
- Safer than C-style strings
- Can be converted to C-style strings

---
### 🛠 Syntax – Declaring and Initializing

```cpp
#include <string>

std::string s1;             // Empty string
std::string s2 {"John"};    // Literal init
std::string s3 {s2};        // Copy init (separate memory)
std::string s4 {"John", 3}; // Joh (first 3 chars)
std::string s5 {s3, 0, 2};  // Jo (from s3 at index 0, length 2)
std::string s6 (3, 'X');    // XXX (repeated char)
```

---
### 🐈 Concatenation

👉 **LEGAL**
```cpp
std::string part1 {"C++"};
std::string part2 {"is a powerful"};
std::string sentence;

sentence = part1 + " " + part2 + " language";
```

🛑 **ILLEGAL**
```cpp
sentence = "C++" + " is powerful";  // C-style string literals can't be added
```

---

### 🔡 Access Characters – `[]` and `.at()`

```cpp
std::string name {"John"};

std::cout << name[1];     // o
std::cout << name.at(0);  // J
```

### 🧵 Iteration

```cpp
std::string name {"John"};
for (char c : name) {
    std::cout << c;
}
```

### 📓 Comparing Strings

Operators: `==`, `!=`, `<`, `>`, `<=`, `>=`

- Compared character-by-character using ASCII values
- Can compare:
    - Two `std::string` objects
    - `std::string` and C-style literals
    - `std::string` and C-style variables

### 🔁 Substrings – `.substr()`

```cpp
std::string s1 {"This is a test"};

s1.substr(0, 4);   // "This"
s1.substr(5, 2);   // "is"
s1.substr(10, 4);  // "test"
```

- First argument: **start index**
- Second argument: **number of characters to extract**

---
### 🚿 Erasing and Clearing – `.erase()` and `.clear()`

```cpp
std::string s1 {"This is a test"};
s1.erase(0, 5);  // "is a test"
s1.clear();      // Empties the entire string
```

---
### 📏 Length – `.length()` / `.size()`

```cpp
std::string s1 {"John"};
s1.length();  // 4
```

- Equivalent to `.size()`
- Returns number of characters in the string

---
### 📍 Searching – `.find()`

```cpp
std::string s1 {"This is a test"};

s1.find("This");   // 0
s1.find("is");     // 2 (first occurrence)
s1.find("test");   // 10
s1.find("pizza");  // std::string::npos
```

- Returns index of first character in match

- If not found: returns `std::string::npos`  
- Optional second argument = start index
    - `s1.find('o', 5);`
#### 🔁 Pattern Example:

```cpp
if (s1.find("pizza") == std::string::npos) {
    std::cout << "Not found!\n";
}
```

### 🧪 Checking Emptiness – `.empty()`

```cpp
std::string s1 {""};
if (s1.empty()) {
    std::cout << "String is empty.";
}
```

---

### 〰 Input – `.getline()`

```cpp
std::string fullName;
std::getline(std::cin, fullName);
```

- `std::cin >>` stops at whitespace and leaves `\n` behind
- `getline()` reads the entire line including spaces

#### 😬 Common Gotcha:

```cpp
int age;
std::string name;

std::cin >> age;
std::getline(std::cin, name);  // gets leftover \n
```

#### 🛠 Fix:

```cpp
std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
```