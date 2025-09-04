♻️ (*MinGW, Windows11, Codelite*)   
 ⌚12:11 am  📆 Tue Aug 12
 🔗 **Related Concepts**: #note #cpp [[Functions - Overview]] , [[Functions - Parameters & Arguments]], [[Type Casting]]
___
## 📝 Note: Functions - Overloading 
Function overloading lets you define multiple functions with the same name, as long as their **parameter lists** are different.
### 🔹 Why?
- Makes code cleaner and more intuitive
- Allows you to use the same function name for related operations that logically belong together, like printing or arithmetic. This keeps your code clean and avoids bizarre, complex naming conventions.
- Improves readability when the function's *concept* is the same, but the data types are different
#### Instead of this ⬇️:
```cpp
void printInt(int x);
void printDouble(double x);
void printString(std::string s);
```
#### You can do this ✅:
```cpp
void print(int x);
void print(double x);
void print(std::string s);
```
#### How, you ask?
When you declare multiple functions with the same name, the compiler uses their signature to tell them apart. **A function signature includes:**
- Function name
- Number of parameters
- Types of arguments

**⚠️ Reminder:** The return type **is not** part of the function signature and cannot be used to distinguish overloads.

> 💡 So even though two functions have the same name, they're treated as completely different functions by the compiler if their parameter lists are different.
### 🔹 Overload Resolution in Action
You can define overloaded functions directly or by using prototypes (forward declarations).
```cpp
#include <iostream>

void print(int value) {
	std::cout << "Integer: " << value << "\n";
}

void print(double value) {
	std::cout << "Double: " << value << "\n";
} 

void print(std::string value) {
	std::cout << "String: " << value << "\n";
}

int main() {
	print(10);   // Calls int version
	print(32.44);   // Calls double version
	print("Hello");   // Calls string version

	return 0;
}
```
### 🔹 **Rules and Behaviors**
1. ✅ Overloaded functions must differ by parameter type, number, or order,
2. ⛔ You **cannot** overload by just changing the return type
3. ✅ Overloading happens at compile time (this is static polymorphism - more on that later)
4. ⚠️ Default arguments can make overloads ambiguous

```cpp
void foo(int x = 10);  // Ambiguous if there's also a foo()
void foo();            // ❌ Compiler error: call to foo() is now ambiguous
```
### 🔹 When **Not** to Use Function Overloading
Function overloading is powerful, but it can hurt more than help when misused. Avoid it when:
- Function meaning diverges too much
- Ambiguity creeps in
- You're tempted to overload everything.

>🧠 _Rule of thumb:_ Overload when the function’s **intent is the same**, but the **type or quantity of data changes**.