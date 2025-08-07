#### 📝 Note: String 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:27 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #cpp #note [[C++ Headers Index]] ,
 [[Standard Template Library]] , [[Variables and Constants]] , [[C++ Syntax Reference]] , [[cstring]] , [[cstdlib]] , [[cctype]] , [[Boolean Logic]]
___
## ✅ What I Know So Far

std::string is a **Class** in the **Standard Template Library**.
- `#include <string>`
- `std namespace`
- Contiguous in memory
- Dynamic in size - (If C-Style strings are like arrays, C++ strings are like vectors).
-  works with iostream
- lots of useful member functions
- familiar operators can be used - see [[Operators]]

Interesting things to dive into:
- Can be converted to C-Style strings if needed
- safer



- Any methods or functions I’ve learned?

---

### 🛠 Syntax - Declaring and Initializing

Unlike C-Style Strings, C++ strings are always initialized.

```cpp
#include <string>

// String                   || Output
std::string s1;             // Empty (No garbage in memory)
std::string s2 {"John"};    // John  (C-Style Literal)
std::string s3 {s2};        // John  (Copied, but two separate strings in mem)
std::string s4 {"John", 3}; // Joh   (The first 3 indices of string)
std::string s5 {s3, 0, 2};  // Jo    (initialized from s3 at 0, 2 is length)
std::string s6 (3, 'X');    // XXX   (constructor.)
```


### 🐈 Concatenation

✅ **LEGAL**
```cpp
std::string part1 {"C++"};
std::string part2 {"is a powerful"};
std::strng sentence;

sentence = part1 + " " + part2 + " language";
// C++ is a powerful language
```

🟥 **ILLEGAL**
```cpp
std::string part1 {"C++"};
std::string part2 {"is a powerful"};
std::strng sentence;

sentence = "C++" + " is powerful";
```
> You cannot concatenate two C-Style string literals, it only works with C++ strings.


### 🔡 Access characters with  `[]` and `.at()` method

```cpp
std::string name {"John"};

std::cout << name[1] << std::endl;     // O
std::cout << name.at(0) << std::endl;  // J
```

### 🧵 Iterating through a String

```cpp
std::string name {"John"};

for (char c: name) {
	std::cout << name;
}
```

### 📓 Comparing

`==` , `!=`, `<`, `>`, `<=`, `>=`

The objects are compared character by character lexically. This means when comparing characters, they use the ascii values to determine the comparative relationship.

Can compare:
- Two `std::string` objects
- `std::string` object and C-Style string literals
- `std::string` object and C-Style string variables

### 🔁 Substrings - `substr()`

Extracts a substring from a std::string

Syntax:
```cpp
object.substr(start_index, length)

std::string s1 {"This is a test"};

std::cout << s1.substr(0,4);  // This
std::cout << s1.substr{5,2};  // is
std::cout << s1.substr(10,4); // test
```

### 📍Searching - `find()`

Returns the index of a substring in a std::string

Syntax
```cpp
object.find(search_string)
```


---

## ❓Open Questions

- What’s the difference between `std::string` and C-style strings?
- Have I seen `std::string_view`? What’s it for?


---

## 

- Unicode/encodings?
- Conversion between string types?
- Performance and memory?