 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚12:15 pm  📆 Sat Sep 20
 🔗 **Related Concepts**: #note #cpp [[string]] , [[C-Style Strings]] , [[String Syntax Reference]] , [[Constants & Constexpr]] , [[Memory Management - Basics]]
___
## 📝 Note: `std::string_view`
#### Initializing objects - type`int`
 Let's begin with something deceptively simple:
```cpp
int x{5};
// vs.
int x = 5;
```
**Both of these tell the compiler**: 
"*Give me a block of memory of the size an `int`, and store value `5` there, and let me refer to that memory as `x`*." **This is clean, fast, and low-cost.**
--- start-multi-column: ID_qh8k
```column-settings
Number of Columns: 2
Largest Column: Standard
Column Spacing: 3px
Border: off
```
#### Initializing objects, type `std::string`
With that in mind, consider ***this*** program:
```cpp
int main() {
  std::string s{"Hello"};
  std::cout << s;
  
  return 0;
}
```
> Simple? Not quite.

When `s` is initialized, it copes the string literal `"hello"` into memory where the`std::string` owns and manages itself. This allocation and duplication is **slower** than dealing with fundamental types like `int`.  We've just made a full `std::string`, only to print and destroy it a moment later.  

--- column-break ---
#### How `std::string` works
```cpp
std::string name{"John"};
```
- The variable `name` lives on the **stack**.
- But the actual **character data** `['J', 'o', 'h', 'n']` lives on the **heap**.
- The string object holds a **pointer** to that heap memory (plus size and capacity).

So when you copy it:
```cpp
std::string name{"John"};
std::string nameCopy{name}; // new heap memory, new copy of text
```
Now we can see that even though it *looks* similar to assigning a value to `int`, it's actually much more complex and expensive.

--- end-multi-column
#### Summary
**Copying a fundamental type like `int` is cheap** because it's just copying a fixed-size value (e.g., 4 bytes) from one memory location to another (stack allocation).  On the other hand, `std::string` is a more complex data type that stores elements in dynamic memory (the heap), which **can grow or shrink at runtime**. The trade-off for this powerful feature is that **heap allocation** is much, much **slower**.  
___
### 🔹 `std::string_view` (C++ 17)
C++17 introduced `std::string_view` to reduce the cost of unnecessary string copies. It lives directly in the `<string_view>` header and acts as a **read-only window** into an existing string. This string ca be:
1. a string literal - `"Hello"`.
2. a `std::string`.
3. another `std::string_view`.

Now, lets rewrite the earlier example:
```cpp
#include <iostream>
#include <string_view>

int main() {
  std::string_view s{"Hello"};
  std::cout << s;
  
  return 0;
}
```
This looks just like the previous example, but there is a key difference. **`s` doesn't own `"Hello"`, it's just viewing it. No allocation, no copy.** 
___
### 🔹 What `std::string_view` is not
Before we define `string_view`, let’s define what it **isn’t**:
- It is **not** a string.   
- It does **not** own the memory it points to.
- It cannot **modify** the characters it views.
- It doesn’t allocate or free memory.
```cpp
std::string_view name{"Jim"}; // ok
name[0] = 'T';                // ILLEGAL - can't modify
name = "Tim";                 // Legal - can reassign view
```
It's best think of `std::string_view` as a pair of pointers:
- One for the beginning of the string
- One for the length

It simply observes part of a string. That's it.
___
### 🔹 Ownership & Lifetime
Because `std::string_view` doesn't own its own data, it's only safe to use as long as the viewed string remains valid.

```cpp
// ...
int main() {
  std::string_view view;
  {
    std::string name{"John"};
    view = name;
  } // name is destroyed leaving view hanging.
}
```
> If you store a `std::string_view` to a temporary or local `std::string`, it can silently become invalid. Always make sure the data its viewing lives long enough.
 ___
### 🔹 `std::string_view` Initialization
As we stated above, a `std::string_view` can be initialized using a C-style string literal, a `std::string`, and an existing `std::string_view`. Here, we will show an example of that in action.
```cpp
#include <iostream>
#include <string>
#include <string_view>

int main() {
  std::string_view s1{"Hello World!"}; // Initialize with C-Style string literal
  std::cout << s1 << '\n';

  std::string s{"Hello World!"}; // Initialize with std::string
  std::string_view s2{s};
  std::cout << s2 << '\n';

  std::string_view s3{s2}; // Initialize with std::string_view
  std::cout << s3 << '\n';

  return 0;
}
```
### Function Parameters with `std::string_view` 
Both a C-style string and a `std::string` will implicitly convert to a `std::string_view`. Therefore, a `std::string_view` parameter will accept arguments of type C-style string, a `std::string`, or `std::string_view`:

```cpp
#include <iostream>
#include <string>
#include <string_view>

void printString(std::string_view str) {
  std::cout << str;
}

int main() {

  printString("Hello "); // Passing a C-string literal argument

  std::string name{"John"}; 
  printString(name); // Passing a std::string argument 

  std::string greeting{", Welcome home!\n"};
  printString(greeting);

  return 0;
}
```
___
### 🔹Function Parameters with `std::string`
Unlike in the section above to use a `std::string_view` as an argument for a function that has a `std::string` parameter (the opposite of above), you would need to **explicitly convert** `std::string_view` or you can create a `std::string` using a `std::string_view` initializer and pass that `std::string` as an argument. 
```cpp
#include <iostream>
#include <string>
#include <string_view>

void printString(std::string test) {
  std::cout << test << '\n';
}

int main() {
  std::string_view arg1{"Testing C-Style Literal"};
  std::string arg2{arg1};

  std::cout << typeid(arg1).name() << '\n';
  std::cout << typeid(arg2).name() << '\n';
  std::cout << typeid(static_cast<std::string>(arg1)).name();

  printString(arg2);
  printString(static_cast<std::string>(arg1));
  return 0;
}
```
### `std::string_view` and `std::string` Function Parameters
Unlike in the last example, where we passed c-string literals and `std::string` arguments through a function with a `std::string_view` parameter, `std::string_view` cannot be *implicitly* converted to a `std::string`, but it can be **explicitly converted**. Like so:
```cpp
std::string_view view{"View"};
std::string string{view};
```
or you can use static_cast:
```cpp
std::string_view view{"View"};
std::string string = static_cast<std::string>(view);
```
Refer back to [[Assignment & Initialization]] for details.
### 🔹Literals for `std::string_view`
Much like how a floating-point literal is a `double` by default, a string literal is a c-style string literal by default. We can create `std::string` literals **and** `std::string_view` literals with the `using` directive:
```cpp
#include <iostream>
#include <string>      // for std::string
#include <string_view> // for std::string_view

int main()
{
    using namespace std::string_literals;      // access the s suffix
    using namespace std::string_view_literals; // access the sv suffix

    std::cout << "foo\n";   // no suffix is a C-style string literal
    std::cout << "goo\n"s;  // s suffix is a std::string literal
    std::cout << "moo\n"sv; // sv suffix is a std::string_view literal

    return 0;
}
```
It’s fine to initialize a `std::string_view` object with a C-style string literal (you don’t need to initialize it with a `std::string_view` literal.

That said, initializing a `std::string_view` using a `std::string_view` literal won’t cause problems (as such literals are actually C-style string literals in disguise).
### 🔹constexpr `std::string_view`
Unlike `std::string`, `std::string_view` has full support for constexpr:
```cpp
#include <iostream>
#include <string_view>

int main()
{
    constexpr std::string_view s{ "Hello, world!" }; // s is a string symbolic constant
    std::cout << s << '\n'; // s will be replaced with "Hello, world!" at compile-time

    return 0;
}
```

This makes `constexpr std::string_view` the preferred choice when string symbolic constants are needed.














___
### 📌 Key Definitions










___
### 🧠 Flashcards

