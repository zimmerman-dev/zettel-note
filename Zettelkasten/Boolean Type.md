♻️ (*MinGW, Windows11, Codelite*)   
⌚10:01 pm  📆 Tue Sep 9  
🔗 **Related Concepts**: #note #cpp  [[Operators - Overview]], [[Control Flow - Overview]], [[Fundamental Data Types]] , [[Boolean Logic]]
___
## 📝 Note: Boolean Type
Ever wonder why spell check always forces you to capitalize "Boolean"? That's because Boolean is a proper noun, named after its inventor **George Boole**.
### 🔹 Boolean Variables
A Boolean variable is an object that can store only two possible values: `true` and `false`. To declare a Boolean variable, we use the keyword `bool`.

```cpp
bool b;
```

To initialize or assign a `true` or `false` value to a Boolean variable, we use the literals `true` or `false`.

```cpp
bool alive{ true }; // Initialization
alive = false;      // Assignment

bool dead{};        // Default initialize to false
```
### 🔹 Boolean Literals
`true` and `false` are **Boolean literals**. Just like `42` is an integer literal or `'a'` is a character literal, `true` and `false` are the only two literal values of type `bool`.
### 🔹 Bool in Memory
Boolean values are not actually stored in memory as the words `true` or `false`. Instead, they are stored as **integral values**, which is why `bool` is considered an integral fundamental data type.  

- In memory: `true` → 1, `false` → 0  
- When evaluated in expressions, Booleans behave as their integer counterparts.

```cpp
#include <iostream>

int main()
{
    std::cout << true << '\n';
    std::cout << !true << '\n';
    
    bool x{ true };
    std::cout << x << '\n';

    return 0;
}
```
> By default, `std::cout` prints `0` for `false` and `1` for `true`.
### 🔹 Using `boolalpha`
`std::boolalpha` (from `<iostream>`) is a **stream manipulator** that changes how Booleans are represented in output.

```cpp
std::cout << (5 > 3);                     // prints 1 (true as numeric)
std::cout << std::boolalpha << (5 > 3);   // prints true
std::cout << std::noboolalpha << (5 > 3); // prints 1 again (reset)
```

- With `std::boolalpha`, Booleans print as `true`/`false` instead of `1`/`0`.
- `std::noboolalpha` resets the stream back to numeric form.
### 🔹 Inputting Boolean Values
```cpp
#include <iostream>

int main()
{
    bool x{};
    std::cout << "Enter a numeric boolean value: ";
    std::cin >> x;
    std::cout << "You entered: " << x << '\n';
    std::cout << x << " is ";
    std::cout << std::boolalpha << x;
}
```

Key considerations:
1. What happens if you enter `1`?  
2. What happens if you enter `0`?  
3. What happens if you enter `5` or a letter, `a`?  

> *See [[Boolean Logic]] for more on `std::boolalpha` and the "truthy/falsey" phenomena.*
### 🔹 Boolean Return Values
Boolean values are often used as the return type for functions that check whether something is true or not. Such functions are typically named starting with *is* or *has*.

```cpp
#include <iostream>

int userInput()
{
    int x{};
    std::cout << "Enter an Integer: ";
    std::cin >> x;
    return x;
}

bool isEqual(int x, int y)
{
    std::cout << "Integer " << x << " and " << y << " are equal?\n";
    return x == y;
}

int main()
{
    int a{ userInput() };
    int b{ userInput() };
    
    std::cout << std::boolalpha;
    std::cout << isEqual(a, b) << '\n';
}
```
___
### 📌 Key Definitions

- **Boolean type (`bool`)**: A fundamental C++ type that stores either `true` or `false`.
- **Boolean literal**: The keywords `true` and `false`, which represent the two possible `bool` values.
- **std::boolalpha**: Stream manipulator that prints bools as `true`/`false` instead of `1`/`0`.
- **Truthy / Falsy**: The idea that non-zero values convert to `true` and zero converts to `false`.

___
### 🧠 Flashcards

**Q:** What are the two Boolean literals in C++?  
**A:** `true` and `false`

**Q:** How does `std::cout` print Boolean values by default?  
**A:** As `1` (true) or `0` (false)

**Q:** What does `std::boolalpha` do?  
**A:** Makes `std::cout` print bools as `true` or `false` instead of `1`/`0`

**Q:** What happens if you assign `5` to a bool?  
**A:** It converts to `true` (any non-zero is true)

**Q:** What type is the result of a comparison expression like `x == y`?  
**A:** `bool`
