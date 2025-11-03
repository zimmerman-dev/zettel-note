 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚9:15 pm  📆 Sun Nov 2
 🔗 **Related Concepts**: #note #cpp [[Type Conversion - Implicit Type Conversion]] , [[Type Conversion - Overview]]
___
## 📝 Note: Type Conversion - Implicit Type Conversion (cont'd)
Earlier, we introduced [[Type Conversion - Implicit Type Conversion]], so let's recap the most important bits first.
- The process of converting data from one type to another is broadly called **Type Conversion**.
- **Implicit Type Conversion** is performed automatically by the compiler when one data type is required, but a different data type is supplied.
- **Explicit Type Conversion** is requested by using a *cast operator* such as `static_cast`.
- Converting a value to another type produces a **temporary object** of the target type, holding the converted result. The original data itself is unchanged.

In this note, we'll focus on the conversion of values to other types of values. We'll cover other types of conversions once we introduce the prerequisite topics (pointers, references, inheritance, etc...)
___
### 🔹 Conversions
The reason conversions matter is the same reason types matter: they tell the compiler how to _interpret bits_.

For instance, the bit pattern `0100 0000 0100 0000 0000 0000 0000 0000` could represent either the integer **1,073,741,824** _or_ the floating-point value **3.0**, depending on the type.

Conversions exist to bridge those interpretations safely. With that in mind, what happens when we do something like this:
```cpp
float f{3}; // Initialize floating point variable with an integer literal?
```





___
### 📌 Key Definitions

___
### 🧠 Flashcards
