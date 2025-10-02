 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚12:14 pm  📆 Sat Sep 20
 🔗 **Related Concepts**: #note #cpp [[String Syntax Reference]] , [[C-Style Strings]] , [[string_view]] , [[Fundamental Data Types]] , [[Memory Management - Overview]]
___
## 📝 Note: string
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
#### Key insights
Unlike the fundamental types like `int`, `char`, `float`, etc., `std::string` can be initialized with a very small value, only to be assigned later with a much larger value. This is the power of the `std::string`! If `std::string` doesn't have enough memory to store a string, it will request additional memory (at runtime) using a form of memory allocation called **dynamic memory allocation**, which we will discuss later in [[Memory Management - Overview]].
___
### 🔹 String input with `std::cin`
Using `std::string` with `std::cin` may yield surprising results! Consider the following program:
```cpp
#include <iostream>
#include <string>

int main() {

  std::cout << "Enter your full name here: ";
  std::string name{};
  std::cin >> name;
  
  std::cout << "Enter your favorite color: ";
  std::string color{};
  std::cin >> color;
  
  std::cout << "Your name is " << name << " and your favorite color is " << color << '\n';
  return 0;  
 }
```
 
 Unfortunately, the output for this seemingly simple program will be this:
 ```bash
$ Enter your full name here: David Jones
$ Enter your favorite color: Blurple
$ Your name is David and your favorite color is Jones
 ```
*What in tarnation?!*

This is because when using the extraction operator `>>`, it only returns characters up to the first whitespace leaving the rest in the buffer for the next extraction.
### 🔹 `std::getline()`
To read a full line of input into a string, you're better of using the `std::getline()` function instead:
```cpp
  std::cout << "Enter your full name here: ";
  std::string name{};
  std::getline(std::cin >> std::ws, name);
```
#### What is `std::ws`?
In [[Floating-Point Types#🔹 `std setprecision()`|Floating-Point Types]], we learned about `std::setprecision()` to change the number of **digits of precision** that `std::cout` displayed. Remember, `std::setprecision()` is what's called an **output manipulator**.

`std::ws` on the other hand, is what known as an **input manipulator** and what it does is tells `std::cin` to ignore any leading whitespace before extraction.

> Note: **Leading whitespace** is any whitespace character (spaces, tabs, or newlines) that occur at the beginning of a string.

 Now, consider this program:
 ```cpp
 #include <iostream>
 #include <string>
 
 int main() {
   std::cout << "Pick 1 or 2: ";
   int choice{};
   std::cin >> choice;
   
   std::cout << "Now, enter your name: ";
   std::string name{};
   std::cin >> name;
   
   std::cout << "Hello " << name << ", you picked " << choice << '\n';
   return 0;
 }
 ```
 > All good right? I mean, we don't have to worry about whitespace in the first extraction because there's no space?
 
❌ **Wrong**
When you the user gets prompted from `std::cin` and they enter a value using the extraction operator, `>>`—even if there are no spaces in what they type—when the user presses **enter**, the terminal sneaks a newline character in, and it stays in the buffer for the next extraction.
#### Best Practice for Now
If using `std::getline()` to read strings, use `std::cin >> std::ws` to ignore leading whitespace. This needs to be done for each `std::getline()` call, as `std::ws` is not preserved across calls.
___
### 🔹 The length of `std::string`
If we want to know how many characters are in a `std::string`, we can ask a `std::string` object for its length. It's a tad *different* than we are used to seeing, though it is relatively straightforward:

```cpp
#include <iostream>
#include <string>

int main() {
  std::string name{"Alex"};
  std::cout << name << " has " << name.length() << " characters in it.\n";

    return 0;
}
```

Although `std::string` is *usually* null-terminated just like a C-style string, the returned length of a `std::string` does not include the null-terminator character. 

Note: Instead of asking for the string length as `length(name)`, we say `name.length()`. The `.length()` function isn't a normal standalone function, but a special type of function nested with `std::string` called a **member function**. We will cover member functions later, but for now the key detail is normal functions, we call `function(object)`. With member functions, we call `object.function()`.

#### An Aside
Also note that `std::string::length()` returns an unsigned integral value (most likely of type `size_t`). If you want to assign the length to an `int` variable, you should `static_cast` it to avoid compiler warnings about signed/unsigned conversions:
```cpp
int length{static_cast<int>(name.length())};
```

Later, consider looking into `std::ssize()`(C++20) at [cppreference.com](https://en.cppreference.com/w/cpp/iterator/size.html)
___
### 🔹 Basic Memory Practice with `std::string`
- Whenever a `std::string` is initialized, a copy of the string use to initialize it is made. Making copies of strings is expensive, so care should be taken to minimize the number of copies made.
- **Do not** pass `std::string` by value. When `std::string` is PBV, the `std::string` function parameter must be instantiated and initialized with the argument. This result is an expensive copy. We'll discuss what to do instead later when talking about `std::string_view`.
#### Returning a `std::string`
When a function returns by value to the caller, the return value is normally copied from the function back to the caller. So you might expect that you *shouldn't* return a `std::string` value; however, as a rule of thumb, that's generally not the case.

It is okay to return a `std::string` value when:
- It resolves to local variable of type `std::string`
- It resolves to a `std::string` that has been returned by value from another function call or operator
- It resolves to a `std::string` **temporary** that is created as part of the return type.
___
### 🔹 `std::string` Literals
Double-quoted string literals are considered C-style string literals, but if we want to use a `std::string` literal, we add the `s` suffix to the end of the double-quoted literal. The most concise way to do this is by `using namespace std::literals`, though by doing so you run the risk of adding a bunch of literals you do not need. So it's actually best if you just need `std::string` literals, to only access `using namespace std::string_literals`.

___
### 📌 Key Definitions










___
### 🧠 Flashcards

