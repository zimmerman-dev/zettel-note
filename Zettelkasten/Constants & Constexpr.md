 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:08 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #note #cpp [[Fundamental Data Types]], [[Variables and Objects]], [[Enums]] , [[Preprocessor Directives]], [[Functions - Parameters & Arguments]], [[Pointers and References]] , [[Compile-time Optimization]]
___
## 📝 Note: `const` and `constexpr`
In C++, a **constant** is any value that cannot change once it’s been set.  
There are two main keywords used to create constants:

- `const`: Marks a variable as **read-only** after initialization.  
- `constexpr`: Requires the value to be **evaluated at compile time**.

> 💡 `constexpr` is stronger — it implies `const`, but also demands compile-time evaluation.
___
### 🔹 Types of Named Constants
In C++, named constants come in a few main forms. These allow you to label and reuse unchanging values throughout your code.
1. **Constant Variables (`const`)**  
     A variable that must be initialized immediately and cannot be modified afterward.    
2. **`constexpr` Constants**  
     A stronger form of constant — must be evaluable at compile time. Covered in detail below.
3. **Object-like Macros**  
     Preprocessor definitions that perform simple text substitution. Avoid when possible.    
4. **Enumerations**  
     Named sets of integer constants. Covered in [[Enums]].
___
### 🔹 `constexpr`: Compile-Time Constants
`constexpr` tells the compiler: *“Evaluate this now — at **compile time**, not at runtime.”* That makes it stronger than `const`, which only guarantees a value **won’t change**, but doesn’t guarantee **when** it’s evaluated.

```cpp
constexpr int width { 5 * 3 };  // Evaluated during compilation
```

> You can use `constexpr` in more places than `const` — like array sizes, template arguments, or in other `constexpr` expressions.

**Rule of Thumb**:  If the value **can be computed at compile time**, prefer `constexpr`.
--- start-multi-column: ID_v8io
```column-settings
Number of Columns: 2  
Largest Column: Standard  
Column Spacing: 3px  
Border: off
```
####  `const`
- Marks a value as **read-only after initialization**
- Value may be known at **runtime**
- Can't be changed, but may depend on runtime input
- Commonly used to protect function parameters or immutable config values
- Can’t be used in places that require compile-time constants (e.g., array size)
```cpp
const int maxInput = getUserInput(); // OK
```

--- column-break ---
#### `constexpr`
- Value must be **fully known at compile time**  
- Compiler is required to evaluate it early  
- Used in expressions, array sizes, and templates    
- Enables **constant folding** and other optimizations   
- Must be initialized with a constant expression
```cpp
constexpr int size = 10 * 2; // ✅

```

--- end-multi-column
___
### 🔹 Declaring Constant Variables
#### `const` variables
Use `const` before the type to create a read-only variable:
```cpp
const int maxUsers{10};
```
- You **must initialize** `const`, at the point of definition
- It **cannot be modified** after initialization
#### `constexpr` variables
Use `constexpr` to declare a compile-time constant:
```cpp
constexpr int bufferSize{512};
```
- Must be initialized with a **compile-time constant expression**
- **Stricter** than `const`, but also more **powerful** 
- Enables optimizations like constant folding
##### Note on style
You are legally allowed to write either `const` and `constexpr` after the type, before the identifier; however, you will go to jail for 100 years if you do don't do it.
```cpp
int const maxUsers{10}; // 🤮
int constexpr minUsers{1}; // 🤮
```
### 🔹 Invalid Declarations (Common Pitfalls)
```cpp
const int x;       // ❌ Error: must be initialized
constexpr int y;   // ❌ Error: must be initialized
x = 5;             // ❌ Error: can't assign later
```
___
### 🔹 Initialization
#### `const` Variable
- Can be initialized with **a literal**, **a non-const**, or **a runtime value**.
- It just means “this can’t be changed **after** it’s initialized.”

```cpp
int runtimeVal{10};
const int a{5};         // ✅ literal
const int b{runtimeVal}; // ✅ non-const
```
#### `constexpr` Variable
- Must be initialized with something the **compiler can evaluate at compile time**.  
- So it must be: 
    - a **literal**        
    - a **constexpr**
    - or a **constexpr function call**

```cpp
constexpr int x{5};              // ✅ literal
constexpr int y{x + 2};          // ✅ another constexpr
constexpr int getVal() { return 7; }
constexpr int z{getVal()};       // ✅ constexpr function

int runtimeVal{10};
constexpr int bad{runtimeVal};   // ❌ not allowed: runtimeVal is not constexpr
```
___
### 🔹 Naming Conventions
Write constants the same way you'd write variables — just make sure the name reflects that it's **fixed**, not computed or changing.

--- start-multi-column: ID_c1g5
```column-settings
Number of Columns: 2
Largest Column: Standard
Column Spacing: 3px
Border: off
```

#### ✅ Recommended Styles

| Style        | Example     | Notes                             |
| ------------ | ----------- | --------------------------------- |
| `camelCase`  | `maxUsers`  | Your preferred default style      |
| `kCamelCase` | `kMaxUsers` | Google-style naming for constants |

--- column-break ---
#### ⚠️ Avoid These
|Style|Example|Why Avoid?|
|---|---|---|
|`ALL_CAPS`|`MAX_USERS`|Reserved for macros in C++|
|Prefixes like `constAge`|`constAge`|Redundant — `const` keyword already signals intent|

--- end-multi-column
📌 _Avoid `constAge`, `constHeight`, or `ConstX` — the `const` keyword already communicates intent. Redundant prefixes aren’t helpful._
___
### 🔹 Constants in Function Parameters
`constexpr` **cannot** be used as a function parameter — but `const` can.
#### Summary Table
--- start-multi-column: ID_2dmo
```column-settings
Number of Columns: 3 
Largest Column: Standard 
Column Spacing: 3px 
Border: off
```
#### Why?
- `constexpr` requires **compile-time evaluation**   
- But function parameters are only known at **runtime**, once the function is called   
- Therefore, they **cannot** be declared `constexpr`


--- column-break ---
#### Syntax
- `T` &nbsp &nbsp &nbsp &nbsp &nbsp &nbsp ----------->
- `const T` &nbsp ---------->
- `T&` &nbsp &nbsp &nbsp &nbsp &nbsp &nbsp ---------->
- `const T&` &nbsp --------->
- `const T*` &nbsp --------->
- `T* const` &nbsp --------->

--- column-break ---
#### Meaning
- A copy, modifiable
- A copy, read-only inside function
- A reference, modifiable
- A reference, read-only
- A pointer to const - value protected
- A const pointer - pointer protected

--- end-multi-column
```cpp
void print(const int x);     // ✅ OK
void print(constexpr int x); // ❌ Error
```

**So when do we use `const`?**
```cpp
void print(const int x) {
  std::cout << x;
}
```
___
### 🔹 Returning Constants (`const` and `constexpr`)
#### `const` Return by Value
You **can** make a return value `const`:

```cpp
const int getValue() {
  return 5;
}
```

But for fundamental types (like `int`, `double`, `char`, etc.), this is **meaningless**:
- The returned value is a **copy**, and the caller can still assign it    
- The `const` is **ignored**, and some compilers may issue a warning    

> **Use `const` only with reference or pointer returns**, where it protects the _referenced_ object.
#### `constexpr` Return
If a function **can be evaluated at compile time**, you can mark it as `constexpr`:

```cpp
constexpr int getConstexprValue() {
  return 10 + 5;
}
```

Now you can use it in constant expressions:
```cpp
constexpr int total = getConstexprValue(); // ✅ OK
```

A `constexpr` function:
- Must have a **single return statement** (if trivial)   
- Must return a value that can be computed at **compile time**    
- Can still be called at **runtime**, if needed

> But the compiler will only evaluate it at compile-time if the context **requires** it (e.g., array size, `constexpr` variable).
___
### 🔹 Object-like Macros vs `const` / `constexpr`
Before modern `const` and `constexpr`, programmers often used **macros** to define constants Here's an example from [[preprocessor directives]]:

```cpp
#define MY_NAME "John"

int main() {
  std::cout << MY_NAME;
}
```
-   The preprocessor **replaces `MY_NAME` with `"John"`**
#### Why Avoid Them?
-   These are just _textual substitutions_ — no type checking or scope
- Harder to debug because they're invisible to the compiler
- Easy to misuse

Prefer:
```cpp
const std::string_view myName{ "John" };
```
___
### 🔹 Constants Across Multiple Files
You’ll often need constants shared across multiple `.cpp` files. But constants have **internal linkage** by default — so each definition is _separate_ in each file. That can cause **duplicate symbol errors** or unexpected behavior.

#### ✅ The Right Way (since C++17)
Use `inline const` in a header:
```cpp
// config.h
inline const int screenWidth{ 1280 };
```

This tells the compiler: "*This cannot be safely defined in multiple translation units.*"
#### ✅ Older Way (before C++17)
Declare in a header with `extern`, and define in one `.cpp`:
```cpp
// config.h
extern const int screenWidth;

// config.cpp
const int screenWidth{ 1280 };
```

This avoids redefinition but requires managing the definition manually.
___
### 🔹 Type Qualifiers: `const`, `volatile`, and Friends
In C++, the `const` keyword is what’s called a **type qualifier** — it modifies the meaning of a type without changing the type itself. Another lesser-used qualifier is `volatile`.

When a type is “qualified,” it means it comes with **special restrictions or guarantees** about how it can be used.
- If something is `const`, it **cannot be modified** after initialization.    
- If something is `volatile`, it tells the compiler:

 *"This value **might change outside the program’s control**, so don’t optimize away reads or writes."*
    
The classic use of `volatile` is for memory-mapped I/O, hardware registers, or multithreaded shared memory where something _external_ (like hardware or another thread) can change a value behind your back.

You’ll rarely use `volatile` unless you’re writing **low-level or embedded code**, but you’ll use `const` everywhere.
___
Together, `const` and `volatile` are sometimes grouped under the umbrella of **cv-qualifiers** (short for _const-volatile_ qualifiers).

So when someone says a type is “cv-qualified,” they mean it’s marked with one or both of those.  
If it has neither, it's “cv-unqualified.”

> Example:
> 
> - `int` is cv-unqualified.     
> - `const int` is cv-qualified.    
> - `volatile int` and `const volatile int` are also cv-qualified.
___
### 📌 Key Definitions
- **Constant**  
    A value that cannot change at runtime (e.g. `const int x{5};`).   
- **Named Constant**  
    A constant associated with an identifier, like `const int size{10};`.   
- **Literal Constant**  
    A fixed value with no name — like `42`, `3.14`, or `"hello"`.  
- **Constant Variable**  
    A variable declared with `const` or `constexpr`; it must be initialized and cannot change. 
- **Type Qualifier**  
    A keyword that modifies a type’s behavior. In this context: `const` and `volatile`.  
- **Const Qualifier**  
    Specifically refers to the use of `const` as a qualifier.  
- **cv-Qualified Type**  
    A type modified by `const`, `volatile`, or both.

---
### 🧠 Flashcards

**What does `constexpr` guarantee about a value?**  
?|?  
It is known and evaluated at compile time.

___

**Can a `constexpr` variable call a runtime function?**  
?|?  
No — its initializer must be a constant expression.

___

**When must a `const` or `constexpr` variable be initialized?**  
?|?  
Immediately, at the point of definition.

___

**What happens if a `constexpr` initializer isn’t constant?**  
?|?  
Compiler error — it violates the rules of compile-time evaluation.

___

**What’s the main difference between `const` and `constexpr`?**  
?|?  
`const` means read-only; `constexpr` means constant **and** known at compile time.

___

**When is `const` on function parameters most useful?**  
?|?  
When used with references or pointers, to prevent side effects.

___

**What does `const int* ptr` mean?**  
?|?  
Pointer to a constant int — you can’t change the value through the pointer.

___

**Why are macros like `#define MAX 10` discouraged?**  
?|?  
They’re untyped, unscoped, and not checked by the compiler.

#flashcards 