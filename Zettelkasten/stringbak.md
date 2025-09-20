 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚10:44 pm  📆 Fri Sep 19
 🔗 **Related Concepts**: #note #cpp
___
## 📝 Note: stringbak
While it's fine to use **C-style string literals**, **C-style string variables** come with their own set of challenges.
- You cannot use assignment to assign C-style string variables new values.
- If you copy a larger C-style string into the space allocated for a shorter C-style string, **UB** will result.

Example of [[C-Style Strings|C-Style String Literals]].
```cpp
#include <iostream>

int main() {
  std::cout << "Hello"; // "Hello" is an example of a C-style string literal
  return 0;
  }
```

In modern C++, C-style strings are best avoided. To mitigate these problems, C++ has introduced two additional string-types into the language:
- `std::string`
- `std::string_view`

`std::string` and `std::string_view` are not fundamental data types like `int`, or `char`. They are considered **class-types**, and we will discuss what that means down the road in [[Classes and Objects(STUB)]].
___
### 🔹 Introducing `std::string`
The easiest way to work with strings in modern C++ is by using `std::string` from the `<string>` header file. In doing so, you can create objects of type `std::string`, as well as assign `std::string` variables with new values just like any other object.

Just like normal variables, you can initialize or assign values to `std::string` objects as you would expect:
```cpp
#include <iostream>
#include <string>

int main() {

  std::string name{"John"};
  name = "Dave";
  std::cout << name << '\n';
  
  return 0;
  }
```




























___
### 📌 Key Definitions










___
### 🧠 Flashcards

