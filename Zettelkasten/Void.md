 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚9:01 pm  📆 Thu Sep 4
 🔗 **Related Concepts**: #note #cpp [[Fundamental Data Types]] , [[Fundamental Data Types]]
___
## 📝 Note: Void
Void - The *easiest* type of the data types to explain. **Void** means "no type".
### 🔹 Incomplete Types
`void` is what is referred to as an **incomplete type**. That means, it's a type that can be declared, but not yet defined. The compiler recognizes the existence of such types, but does not have enough information to determine how much memory to allocate for objects of the type. Because of this, incomplete types can not be instantiated, which means you can't define an object variable with the incomplete `void` type.

```cpp
void value; // ⛔ Won't work.
```

However, `void` *can* be used in other ways.
### 🔹 `void` Functions 
`void` is most often used to indicate that a function **does not return a value** see [[Functions - Return]]. 

```cpp
#include <iostream>

void printSomething()
{
	std::cout << "This function doesn't return a value!\n";
}

int main()
{
	printSomething();

	return 0;
}
```
### 🔹 Deprecated:
In C, `void` is used as a way to indicate that a function does not take parameters.
```cpp
int getValue(void) // void indicating no parameters
{
	int x{};
	std::cin >> x;
	
	return x;
}
```
> This will compile in C++ (for backwards compatibility reasons), this use of the `void` keyword is considered deprecated for C++.
### Advanced `void` use
Later, we will consider void pointers.
___
### 🧠 Flashcards

