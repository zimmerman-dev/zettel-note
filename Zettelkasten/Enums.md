#### 📝 Note: Enums 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:11 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #note #cpp [[Constants]], [[Data Types]], [[Type Casting]]
___
## 🧾 C++ Enum Notes
### 🔹 What is an `enum`?
An `enum` (short for *enumeration*) is a **user-defined data type** used to name a set of related **integral constants,** (usually `int` by default). 

- `char`, `short`, `int`, `long` ✅ **Legal types for enums**
- `float`, `double`, `long double` ⛔ **Illegal types for enums**
#### Why?
Enums improve readability and avoid "magic numbers." Use them when you have a fixed set of known values (like menu choices, states, or commands) that won’t change often.
##### Syntax:
```cpp
enum EnumName {
Enumerator1,
Enumerator2,
...,
};
```
>To create one, use the `enum` keyword, followed by the name of the enum, separating the enumerators with commas:

Example:
```cpp
enum TaskOption {
Add,
View,
Summary
};
```
>In the example above, we **define a new type**  `TaskOption` with **three constants**:
- `Add` --------> `0`
- `View` -------> `1`
- `Summary` ---> `2`
___
### 🔹 Underlying Values
By default, the first name is assigned `0`, and they count up from there unless otherwise stated. you can manually override this:
```cpp
enum TaskOption {
Add = 2,
View,
Summary
};
```
>In this example, we assign the first name `Add` with `2`. Since enum values count up, `View` is defaulted to `3`, and so on.

You can also just assign all the of then outright:
```cpp
enum TaskOption {
Add = 100,
View = 23,
Summary = 5
};
```

You can also change the **underlying type** (e.g., `char`, `short`, etc.):
```cpp
enum TaskOption : char {
Add = 'A',
View = 'V',
Summary = 'S'
};

// To print these out:
TaskOption choice = Add;
std::cout << static_cast<char>(choice); // prints 'A'
```
---
### 🔹 Using Enums
An enum variable can only hold **one value at a time**, but it can be reassigned.

- Declare a variable of your enum type:
```cpp
TaskOption choice {View}; // Holds the enum value View (1)   
```
- And reassign it freely later:
```cpp
choice = Add; // Follows the same rules of reassignment as noraml variables
```
---
### 🔹 User Input & Enums
`std::cin` doesn't understand enum names directly. Clever work-around:
1. Take user input as an `int` or `char`
2. Map that input to a valid enum value manually (via `if/else` or `switch`).
```cpp
choice = Add;

int input {};
std::cin >> input;

if (input == 1) choice = Add;
else if (input == 2) choice = View;

/*----------------------------------- OR -----------------------------------------*/

switch (input) {
    case 1: choice = Add; break;
    case 2: choice = View; break;
    case 3: choice = Summary; break;
    default: std::cout << "Invalid option\n";
}
```
💡 _Note:_ Enums don't automatically support input/output. They must be **converted** to/from a type like `int` or `char`.
### 🧭 Where Should You Define an `enum`?
You can define an enum:
1. **Outside of** `main()` *(most common)*
2. **Inside of** `main()` *(legal, but often limiting)*
#### ✅ Defining Outside `main()`
```cpp
enum TaskOption {
Add,
View,
Summary
};

int main() {
TaskOption choice {View};
// ...
return 0;
}
```
**Why is this method preferred?**
- Makes the enum visible **globally** (all the functions in your file can access it).
- Keeps your type definitions organized and centralized (Later when we talk about macros, define, const this will make more sense).
- Makes future reuse easier (e.g., if you split your menu into separate functions).

>🔧 _Think of this like defining a custom data type — you wouldn’t want that locked inside `main()`._
#### 😐 Defining Inside `main()`
```cpp
int main() {
	enum TaskOption {
		Add,
		View,
		Summary
	};
	TaskOption choice {View};
	// ...
	return 0;
}
```
**This Works**, but:
- Makes the enum visible only **locally** (Only code *inside* `main()` can see it).
- Can't reuse in other functions
- Makes refactoring a pain in the balls
- Can feel "buried" in a large function
#### 🧪 Side Note: Function Scope vs Global Scope
You *can* technically define an enum inside any block scope, like inside a function, loop, or class, but it's rarely worth doing so unless you're isolating something on purpose. General rule of thumb is to define enums globally if they describe general concepts used across functions.
___
### 🔚 `#define` vs `const` vs `enum`

| Feature         | `#define`            | `const`                     | `enum`                     |
| --------------- | -------------------- | --------------------------- | -------------------------- |
| Type-safe?      | ❌ No                 | ✅ Yes                       | ✅ Yes (sort of*)           |
| Has a type?     | ❌ Just text replaced | ✅ Strong type               | ✅ Becomes `int` by default |
| Scope-aware?    | ❌ Global only        | ✅ Scoped                    | ✅ Scoped if global/local   |
| Debuggable?     | ❌ Hard to debug      | ✅ Shows in debugger         | ✅ Shows in debugger        |
| Named grouping? | ❌ No                 | ❌ No                        | ✅ Groups related constants |
| Const expr?     | ❌ Not evaluated      | ✅ Evaluated at compile-time | ✅ Same                     |
### 🚀 **`enum` vs `enum class`**
TBD