 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚10:11 am  📆 Sun Sep 28
 🔗 **Related Concepts**: #note #cpp
___
## 📝 Note: Bit Manipulation - Overview
As you already know, the **byte** is the smallest *addressable* unit of memory available (See: [[Memory Management - Overview]]). This means that Boolean types that only need 1 bit still occupy a full byte, leaving 7 unused bits. For most modern applications this isn’t a problem, but sometimes it can be useful to *pack* Boolean values into a single byte for efficiency.

**Bit manipulation** is the process of modifying individual bits in an object, and C++ gives us tools to do exactly that.
___
### 🔹 Bit Flags
Normally we treat variables as holding a single value:
```cpp
int num{3};
char letter{'A'};
double pi{3.14159};
```

But we can also treat each bit in an object as an independent Boolean value. When used this way, the bits are called **bit flags**. In other words, one variable can act like many small switches.

- A bit with `0` is **false**, **off**, or **cleared**.  
- A bit with `1` is **true**, **on**, or **set**.  
- Changing a `0` to `1` is called **setting** a bit.  
- Changing a `1` to `0` is called **clearing** a bit.  
- **Flipping** or **inverting** means toggling a bit’s value.  
___
### 🔹 Using `std::bitset`
A **bitset** stores a fixed number of bits, each either `0` or `1`. You can think of it as an array-like object of Boolean values, but optimized for space and efficiency.
```cpp
#include <bitset>

std::bitset<N> name{};
```

- Must include the `<bitset>` header.  
- `N` is a non-negative integer known at compile time.  
- `name` is the identifier of your bitset object.  
#### Example:
```cpp
std::bitset<8> myBitSet{0b10010101};
```
This creates an 8-bit set initialized with `10010101`.  
Even though we haven’t covered classes yet (see: [[Classes and Objects(STUB)]]), you can treat `std::bitset<N>` like a small custom-built container.

#### Bit Position
```text
7 6 5 4 3 2 1 0 : Bit positions
1 0 0 0 1 0 1 0 : Bit sequence
```

Index 0 is the least significant bit. Example:
```cpp
std::bitset<8> bin{0b10001010};

bin[7] == 1  // 128's place
bin[3] == 1  // 8's place
bin[1] == 1  // 2's place
```
#### Why It Feels Array-like
You can access and modify bits with the subscript operator:  
  ```cpp
  myBitSet[1] = 1;
  myBitSet[7] = 0;
  ```
> The size is fixed at compile time. You cannot resize a `bitset` at runtime.  
___
### 🔹 Member Functions
Some of the most common member functions:  

- `.test(pos)` → Returns a **bool**, true if the bit at `pos` is set.  
- `.set(pos)` → Sets a bit (or all bits if no argument). Returns a **reference** to the bitset so you can chain operations.  
- `.reset(pos)` → Clears a bit (or all bits if no argument). Returns a **reference** to the bitset.  
- `.flip(pos)` → Flips a bit (or all bits if no argument). Returns a **reference** to the bitset.  
#### Example:
```cpp
std::bitset<4> bin{0b0101};

bin.set(2);    // set bit 2
bin.reset(1);  // clear bit 1
bin.flip(0);   // flip bit 0
```

These operations are efficient because the bits are packed tightly in memory.
___
### 🔹 Naming Bit Flags
You can assign meaningful names to bit positions with constants. This makes the code easier to read when bits represent real states:

```cpp
std::bitset<4> bin{0b0101};

constexpr int isHappy{0};
constexpr int isSad{1};
constexpr int isMad{2};
constexpr int isSleepy{3};

bin.flip(isSleepy);
```
___
### 🔹 Querying a Bitset
There are several ways to gather information from a bitset:  

- `.size()` → Returns the number of bits (an **integral value**).  
- `.count()` → Returns the number of set bits (an **integral value**).  
- `.all()` → Returns **true** if all bits are set.  
- `.any()` → Returns **true** if at least one bit is set.  
- `.none()` → Returns **true** if no bits are set.  
#### Example:
```cpp
std::bitset<8> bits{0b0000'1101};

std::cout << bits.size() << " bits total\n";   // integral result
std::cout << bits.count() << " bits are set\n"; // integral result

std::cout << std::boolalpha;
std::cout << "All bits set? " << bits.all() << '\n';   // bool result
std::cout << "Any bit set? " << bits.any() << '\n';    // bool result
std::cout << "No bits set? " << bits.none() << '\n';   // bool result
```
___
### 🧠 Flashcards

What is bit manipulation?  
?|?  
The process of modifying or querying individual bits in an object.

---

What is a bit flag?  
?|?  
An individual bit in a variable treated as a Boolean value (on/off).

---
 
What do “set”, “clear”, and “flip” mean in the context of bit flags?  
?|?  
Set = change `0 → 1`. Clear = change `1 → 0`. Flip = toggle a bit’s value.

---

How is a bitset similar to an array?  
?|?  
You can index into it with `[]` and modify elements, but its size is fixed at compile time.

---

Which member functions can modify bits in a `std::bitset`? What do they return?  
?|?  
`.set()`, `.reset()`, `.flip()`. Each returns a reference to the bitset.

---

Which member functions provide information about bits, and what do they return?  
?|?  
- `.test()` → bool for a single bit.  
- `.size()` → integral, total bits.  
- `.count()` → integral, number of bits set.  
- `.all()` / `.any()` / `.none()` → bool results.


#flashcards