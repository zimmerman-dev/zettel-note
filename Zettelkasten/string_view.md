 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚12:15 pm  📆 Sat Sep 20
 🔗 **Related Concepts**: #note #cpp [[string]] , [[C-Style Strings]] , [[String Syntax Reference]] , [[Constants & Constexpr]] , [[Memory Management - Overview]]
___
## 📝 Note: `std::string_view`
`std::string_view` is a lightweight, non-owning read-only view of a character sequence. As you read on, we will discuss the differences between `std::string` and `std::string_view` and why it's important.
#### Initializing objects - type`int`
 Let's begin with something deceptively simple:
```cpp
int x{5};
// vs.
int x = 5;
```
**Both of these tell the compiler**: 
"*Give me a block of memory of the size an `int`, and store value `5` there, and let me refer to that memory as `x`*." **This is clean, fast, and low-cost.** See: [[Assignment & Initialization]].
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

When `s` is initialized, it copies the string literal `"hello"` into memory where the `std::string` owns and manages the data. This allocation and duplication is **slower** than dealing with fundamental types like `int`.  We've just made a full `std::string`, only to print and destroy it a moment later.  

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
#### TL;DR
**Copying a fundamental type like `int` is cheap** because it's just copying a fixed-size value (e.g., 4 bytes) from one memory location to another (stack allocation).  On the other hand, `std::string` is a more complex data type that stores elements in dynamic memory (the heap), which **can grow or shrink at runtime**. The trade-off for this powerful feature is that **heap allocation** is much, much **slower**.  
___
### 🔹 `std::string_view` (C++ 17)
C++17 introduced `std::string_view` to reduce the cost of unnecessary string copies. It lives directly in the `<string_view>` header and acts as a **read-only window** into an existing string. This string can be:
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
- It's **not** a string.   
- It **doesn't** own the memory it points to.
- It cannot **modify** the characters it views.
- It doesn’t allocate or free memory.
```cpp
std::string_view name{"Jim"}; // ok
name[0] = 'T';                // Error - Invalid operation
name = "Tim";                 // Legal - can reassign view
```
It's best think of `std::string_view` as a pair of pointers:
- One for the beginning of the string
- One for the length

It simply observes part of a string. That's it.
___
### 🔹 Safe Usage & Lifetime (Analogy)
Let’s sidebar for an analogy. Say you want to paint a picture of a bicycle. You’ve got paint and a canvas, but you don’t own a bike to model from. **You have two options:**

- **Buy your own bike.** It’s expensive, but it’s yours. You can decorate it, ride it, or leave it parked wherever and whenever you want. It will always be available for your painting session.
    - 🟥 This is like using a `std::string`: You _own_ the data. It’s flexible, powerful—but has a cost.
    
- **Use your neighbor’s bike.** It’s already sitting outside, shiny and red, perfect for your painting. No need to buy one. But here’s the catch: you can’t move it, modify it, or control how long it stays there. If your neighbor puts it in the garage halfway through your session, you’re out of luck.
    - 🟦 This is like using a `std::string_view`: You _borrow_ the data. It’s lightweight and cheap—but risky if the original disappears.

 💡 **Moral of the story:** 
 > Use your neighbor’s bike (`std::string_view`\) only if you’re sure it’ll still be there when you need it. Otherwise, get your own, i.e., (`std::string`\).
*(From Learncpp.com)*
### 🔹 From Bikes to Bytes: Making the Analogy Real
Let's map this bicycle story directly to how `std::string` and `std::string_view` behave in code:
#### Using `std::string`: Buying your own code
- You make a copy of the string data. That data lives as long as the string object does.
- You can modify it (decorate it).
- You own it. It's safe, reliable, and always available during the object's lifetime.
```cpp
std::string myName = "Tom";
myName[0] = 'D';
```
> Safe: `std::string` Because you own it, you don't have to worry about it disappearing.
#### Using `std::string_view`: *Viewing* your neighbor's bike
- You don't have to make a copy, you just point to some existing string.
- It's lightweight and fast to create.
- But if the string you're viewing goes out of scope, you're left pointing at nothing.
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
> If you store a `std::string_view` to a temporary or local `std::string`, it can silently become invalid. Always make sure the data it's viewing lives long enough.
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

--- start-multi-column: ID_zpco
```column-settings
Number of Columns: 2
Largest Column: Standard
Column Spacing: 3px
Border: off
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

--- column-break ---
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

--- end-multi-column
### 🔹 Function Parameters (Wrapped Up)
Unlike in the last example, where we passed c-string literals and `std::string` arguments through a function with a `std::string_view` parameter, `std::string_view` cannot be *implicitly* converted to a `std::string`, but it can be **explicitly converted**. Like so:
```cpp
std::string_view view{"View"};
std::string string{view};

// or you can use static_cast: 

std::string_view view{"View"};
std::string string = static_cast<std::string>(view);
```
Refer back to [[Assignment & Initialization]] for details.
___
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
___
### 🔹Constexpr `std::string_view`
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
### 🔹 Summary (When to use `string_view` vs `string`)
First, why does `std::string` make such an expensive copy of it's initializer? 
- When an object is **instantiated**, memory is allocated for that object to store whatever data it needs throughout its lifetime. 
- The memory is reserved for the object, and guaranteed to exist as long as the object does, and once the initialization value is copied, the object is no longer reliant on the initializer in anyway.

Let's refer to this example:
```cpp
#include <iostream>
#include <string>

void printString(std::string str) // str makes a copy of its initializer
{
    std::cout << str << '\n';
}

int main()
{
    std::string s{ "Hello, world!" };
    printString(s);

    return 0;
}
```
When `printString(s)` is called, `str` make an expensive copy of `s`. The function prints the copied string and then destroys it. In this case, `std::string_view` is perfect to use instead as function parameter, but there are three criteria needed to assess for this:
1. Could `s` be destroyed while `str` is still using it? 
2. Could `s` be modified while `str` is still using it?
3. Does `str` modify the string in some way that the caller would not expect?

Since all three of these questions are false, we can safely assume that `std::string_view` would be a preferable alternative than an expensive copy. Let's change the above example:

```cpp
#include <iostream>
#include <string>
#include <string_view>

void printString(std::string_view str)
{
  std::cout << str << '\n';
}

int main() 
{
  std::string s{ "Hello, World!" };
  printString(s);
  
  return 0;
}
```
### 🔹 When not to use `std::string_view`
Example 1 (Similar example found here [[string_view#🔹 Safe Usage & Lifetime (Analogy)| Safe Usage & Lifetime]])
```cpp
#include <iostream>
#include <string>
#include <string_view>

int main()
{
    std::string_view sv{};

    {
        std::string s{ "Hello, world!" }; 
        sv = s; 
    } 

    std::cout << sv << '\n'; // undefined behavior

    return 0;
}
```
Here we see a `std::string` constructed locally with a nested block, and within that block we have `sv` reassigned to `s`. After the nested block, `s` is destroyed and `sv` is now viewing an invalid string.
___
### 🧠 Flashcards
  
What is the key difference between `std::string` and `std::string_view` in terms of memory ownership?  
?|?  
`std::string` owns and manages its own memory (heap allocation), while `std::string_view` is a lightweight, non-owning view into existing memory.

---

What happens if a `std::string_view` outlives the string it was viewing?  
?|?  
The view becomes _dangling_—it points to invalid memory, causing undefined behavior if accessed.

---

What are the three safe-use criteria you should check before replacing a `std::string` function parameter with a `std::string_view`?  
?|?  
1. Will the original string be destroyed while the view is still in use?
2. Could the original string be modified while the view is still in use?
3. Does the function modify the string in ways the caller might not expect?
If all are false, `string_view` is likely safe.

---

Can a `std::string_view` be implicitly converted to a `std::string`?  
?|?    
No. You must explicitly convert it using `std::string{view}` or `static_cast<std::string>(view)`.

---
 
 Is this a safe usage of `std::string_view`?

```cpp
std::string_view sv; 


{     std::string s{ "Hello" };     sv = s; } // sv used here
```
?|?  

No. `s` is destroyed at the end of the block, leaving `sv` dangling. Accessing `sv` after that is undefined behavior.

---

Why is `std::string_view` often preferred in `constexpr` contexts?  
?|?   
Because `std::string` cannot be `constexpr`, but `std::string_view` can—making it ideal for compile-time string constants.

---

What type of string literals do these suffixes produce?
- `"foo"`
- `"foo"s`  
- `"foo"sv`  
    ?|?   
- `"foo"` → C-style string (`const char*`)    
- `"foo"s` → `std::string`  
- `"foo"sv` → `std::string_view` 

---

How does `std::string_view` improve performance in function parameters?  
?|?  
It avoids expensive heap allocations and copies by referencing existing string data instead of creating a new copy.

#flashcards 