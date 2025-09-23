 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚10:27 pm  📆 Mon Sep 22
 🔗 **Related Concepts**: #note #cpp
___
## 📝 Note: Constructors and Destructors

### 🔹Constructors
A **constructor** is a special function that **creates and sets up an** object when it's declared.

**When you write something like this**:
```cpp
std::string name{"John"};
```
This constructor process happens automatically.
#### Think of it like this:

If `std::string` is a house blueprint 🏠,  
the **constructor** is the construction crew 👷‍♂️ that _builds_ the house and _furnishes_ it with initial data.
#### C++ Constructors Always:
- Have the **same name** as the class  
- **Don’t have a return type** 
- Can be **overloaded** (multiple versions for different inputs)

```cpp
class Dog {
public:
  Dog(std::string_view n) {
    name = n;
  }

private:
  std::string name;
};
```




















___
### 📌 Key Definitions










___
### 🧠 Flashcards

