#### 📝 Note: Enums 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:11 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #note #cpp [[Data Types]] , [[Variables and Constants]] , [[C++ Syntax Reference]] , [[Statements and Expressions]] , [[Operators]] , [[Type Casting]]
___
## ✅ Enum Learning Plan

### 1. **What is an Enum?**
An `enum` (short for *enumeration*) is a way to give names to a list of related **constant integer values**. They make code easier to read and maintain, and should only be used when you have values that you know aren't going to change.

To create one, use the `enum` keyword, followed by the name of the enum, separating the enum items with commas:
```cpp
enum names {
Tammy,
Sammy,
Cammy,
Steve
};
```
    
- `enum` vs `#define` vs `const`
    

### 2. **Declaring and Using an Enum**

- Basic syntax
    
- Naming conventions
    
- How the compiler assigns values (starts at 0 unless set)
    

### 3. **Practical Use Case**

- `switch` statement with an `enum`
    
- Common patterns (e.g., `enum class`, scoping, preventing collisions)
    

### 4. **Behind the Scenes**

- How enum values are stored (int by default)
    
- Can you change the underlying type?
    
- Can you output enum names with `std::cout`?
    

### 5. **`enum` vs `enum class`**

- Scoped vs unscoped
    
- Type safety
    
- Use cases