 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚3:13 pm  📆 Sat Sep 13
 🔗 **Related Concepts**: #note #cpp
___
## 📝 Note: Introduction to Type Conversion and static_cast
Consider the following program:
```cpp
#include <iostream>

void print(double x) {
  std::cout << x << '\n';
}

int main() {
  
  int num{ 5 };
  print(x);

  return 0;
}
```

Here's a question. When `x` is output to the terminal, is and `int`? Or is it a `double`?
### 🔹 Implicit Type Conversion
In the above example, the `print()` function has a parameter type `double`, but the caller is **passing the value** `5` (type `int`). Take the same program and add this line to the function:
```cpp
void print(double x) {
  std::cout << x << '\n';
  std::cout << typeid(x).name(); // This line will tell you the type of 'x'.
}
```

In most cases, C++ will allow us to *convert* values of one fundamental type to another fundamental type. This process is what's called **type conversion**. If you haven't already, run the first, un-edited program in the debugger. Rather than setting any specific breakpoints, just press F11 (Visual Studio), and *step into* `main()`. Add `num` and `x` to watch window.



























___
### 📌 Key Definitions










___
### 🧠 Flashcards

