 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚9:52 pm  📆 Tue Aug 26
 🔗 **Related Concepts**: #note #cpp [[Statements and Expressions]] , [[Variables and Objects]] , [[Memory Management - Basics]]
___
## 📝 Note: Uninitialized Variables & Undefined Behavior
### Uninitialized Variables - Important Rules!
- In **C/C++**, local variables are **not automatically initialized**.
    
```cpp
int x;   // ❌ contains garbage until initialized
```

- **Global variables**, however, _are_ automatically initialized to zero **if** no explicit initializer is provided.  
    _(We’ll get into globals later.)_
- When a variable is declared but **not initialized**, the memory at its address already holds **whatever random bits** were there before. That’s your **“garbage value.”**
---
### ⚡ Key Definitions
- **Initialized** → The object **was** given a value **at the point of definition**.
- **Uninitialized** → The object **hasn’t been assigned** a known value yet.
- **Assigned** ≠ **Initialized** → Assigning a value later **doesn’t retroactively make it initialized at declaration**.
```cpp
int x;      // Declared, but uninitialized
x = 1;      // Assigned later ✅ no longer uninitialized

int i {1};  // ✅ Properly initialized at declaration
```
> ⚠️ Using uninitialized variables is **one of the most common beginner mistakes**.
---
## Undefined Behavior (UB)
Using the value from an **uninitialized variable** is our first example of **undefined behavior**.

**Undefined Behavior** (UB) = when the **C++ standard** provides **no guarantees** about what happens.  

In other words:
> The compiler _doesn’t know_ what’s supposed to happen…  
> and therefore _anything_ can happen.
---
### 🤒 Symptoms of UB
Your program **might**:
1. Produce different results every run.
2. Produce the **same wrong** result every time.
3. Behave inconsistently depending on inputs.
4. **Look correct** but quietly generate bad data.
5. Crash immediately 💥 … or hours later.
6. Work on **one compiler** but fail on another.
7. Work fine… until you change **something unrelated**.

> 💡 **The insidious part:**  
> UB doesn’t always **look** broken. Sometimes it “works” — until it doesn’t.
---
### Quick Mental Model — **Schrödinger’s Box 🧠**
_(Keeps the concept sticky without breaking your tone.)_

Think of an uninitialized variable as a **sealed box**:
- You **know** the box exists ✅
- But you have **no idea** what’s inside ❌
- Inside could be:
    - 🎁 A valid value
    - 🧨 A crash trigger
    - 🦑 Random garbage data
    - 
Until you **put a value in** (initialize it), **opening the box** (using the variable) = **chaos**.
---
## Best Practices

Always initialize variables:
```cpp
int x{};    // ✅ modern C++ zero-initialize
int y = 0;  // ✅ explicit assignment
```
> Prefer brace `{}` initialization (C++11+).

Use compiler warnings:
```cpp
g++ -Wall -Wextra -Wuninitialized main.cpp
```
---
### 🧠 Flashcards
What is an initialized variable?|||A variable declared and assigned a value upon its creation. 

What happens if you use an uninitialized variable?|||It triggers **undefined behavior** — unpredictable results 

T/F - Local variables auto-initialized in C++?|||❌ No, they hold **indeterminate garbage values**. 

Best way to safely initialize variables?|||`int x{};  // ✅ zero-initialize` 

How to catch UB at compile time?|||`g++ -Wall -Wextra -Wuninitialized` 
#flashcards

