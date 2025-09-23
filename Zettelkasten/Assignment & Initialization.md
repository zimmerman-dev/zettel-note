 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚6:05 pm  📆 Mon Sep 22
 🔗 **Related Concepts**: #note #cpp
___
## 📝 Note: Assignment & Initialization
In [[Statements and Expressions]], we laid a surface-level foundation on what assignment is, and we’ve alluded to initialization in different parts of this notebook. In this note, we plan to dive deeper into both concepts so we can connect them with the fundamentals of memory management down the road.

Before going further, I recommend checking out:  
[[Mixed Expressions & Type Conversions & Promotion]] and [[Introduction to Type Conversion and static_cast]].
___
First, let's recap a basic distinction:
- **Assignment** happens *after* a variable is defined.
- **Initialization** is part of the variable's definition itself.

```cpp
int x = 1; // Initialization: giving the first value to a variable at the point of definition.
x = 2;     // Assignment: giving a new value to an existing variable.
```
### 🔹 Assignment vs. Initialization
At a glance, assignment and initialization can look similar. They often use the same operator (`=`), and both give values to objects. But semantically, they’re very different. Understanding that difference becomes critical as you get deeper into type conversions, temporaries, and memory semantics.
--- start-multi-column: ID_gtdw
```column-settings
Number of Columns: 2
Largest Column: Standard
Column Spacing: 3px
Border: off
```
#### Initialization
When you give a named object an initial value at the point of definition, this is called **initialization**.

```cpp
int value = 42; // ✅ Initialization
std::string name{"Tim"}; // ✅ Also initialization
```
> *This is when the object is being* **constructed**. *This matters for user-defined types like `std::string`, where* **constructors** *get called*.

--- column-break ---
#### Assignment
After the object has been initialized, you would assign the object with a value that replaces the current contents:
```cpp
int value = 42; // Initialization
value = 43;     // Assignment
```
> *In the second line, you're not **defining** `value`, you're modifying it*. 

--- end-multi-column
### 🔹Forms of Initialization
C++ offers multiple forms of initialization. They may look stylistically different, but the differences go deeper. They affect how the compiler treats conversions, whether narrowing is allowed, and how the object is constructed under the hood.
#### Copy Initialization
**Copy initialization** is likely the most common way to initialize a named object, though admittedly, it has sort of fallen out of favor in modern C++ for type safety reasons, which is something we will cover in it's own section. It's called "copy initialization" because the compiler creates a [[Functions - Scope, Lifetime, and Temporaries#🔹 Temporary Objects| temporary]], and that temporary gets moved (or *copied*) into the named object.
```cpp
std::string name = "Tim";
```
What happens:
1. `"Tim"` is implicitly converted to a temporary `std::string`
2. The temporary is moved (or copied) into `name`
3. The temporary is obliterated at the end of the expression (`;`)
#### Direct Initialization
You can imagine why **direct initialization** is named what it is. Because the compiler constructs the object directly using the initializer, there is no temporary object in between. To simplify, rather than creating a temporary, direct initialization "takes out the middleman" and hands the value to the constructed object.
```cpp
std::string name("Tim"); 
```
What happens:
1. The compiler constructs `name` directly in place,  with the given argument.
2. No temporary, no copy. Just straight to construction.
___
### 🔹 3. Why Do These Forms Exist? (Type Safety & Conversions)

Ultimately, there is tradeoff between the different types of conversion. If both copy and direct initialization are valid ways to give an object its first value, why does C++ need multiple styles? It turns out, the _way_ you initialize something can affect:
- whether **type conversions** are allowed,
- whether **narrowing** conversions (like `double` to `int`) are blocked,  
- and whether you're calling an **explicit** or **implicit** constructor.  

This section introduces the reason these patterns exist — and sets the stage for **brace initialization**, which was introduced in C++11 to bring **type safety** and **uniformity** to initialization.
#### Example: Silent Truncation
```cpp
int value = 4.5;   // Compiles fine, but truncates silently
std::cout << value << '\n'; // Outputs: 4
```
> This uses **copy initialization**, and even though you're assigning a `double` to an `int`, the compiler allows it. It truncates the decimal part, and you get `4`.

But what if you _don’t_ want the compiler to make that decision for you?
#### Narrowing Not Allowed
**Brace initialization** is a form of direct initialization, but unlike direct initialization with parentheses, it mostly **forbids narrowing conversions** like `double` to `int`.
```cpp
int value{4.5}; // ❌ Compile Error: Narrowing Conversion
```
> Brace initialization is a kind of strict form of initialization. 
### 🔹Brace Initialization
Brace initialization, also called **uniform initialization**, was introduced in C++11 as a way to bring consistency, safety, and readability to initialization. It uses curly braces (`{}`) instead of parentheses or equal signs.
```cpp
int x{5};                // Ok: Brace Initialization
std::string name{"Tom"}; // Ok: std::string constructor with Brace Initialization 
```

The goal was to fix a few long-standing quirks in C++:
- Avoid **narrowing conversions**
- Make initialization syntax more consistent
- Reduce ambiguity with constructors
- Work across all types (fundamental, arrays, structs, classes)
#### Why It’s Called “Uniform”
You can use `{}` with almost anything:
```cpp
int x{5};                             // Fundamental
std::vector<int> v{1, 2, 3};          // STL container
MyStruct s{1, 2};                     // Struct/class
int arr[3]{1, 2, 3};                  // Array
```
> The syntax doesn’t change. That’s why it’s called **uniform**.
#### Narrowing is Not Allowed
The most famous feature of brace initialization is that it **refuses to compile** if you try to initialize a variable in a way that could cause data loss.
```cpp
int x{4.5};   // ❌ Error: narrowing conversion from double to int
```
**This is intentional. It's the compiler saying:**
*“You’re asking me to do something risky. You better make it explicit.”*

If you really want to allow it, you can use a `static_cast` or go back to copy/direct initialization.
___
### 📌 Key Definitions










___
### 🧠 Flashcards

