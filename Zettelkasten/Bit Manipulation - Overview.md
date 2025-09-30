 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚10:11 am  📆 Sun Sep 28
 🔗 **Related Concepts**: #note #cpp
___
## 📝 Note: Bit Manipulation - Overview
As you already know, the **byte** is the smallest *addressable* unit of memory available (See: [[Memory Management - Basics]]). This means that Boolean types that only need 1 bit to store, 7 other bits are *unused*. For the most part, this isn't really a problem for modern computers; however, in some cases it can be useful to *pack* 8 Boolean values into a single byte for efficiency purposes.

**Bit manipulation** is the process of modifying individual bits in an object, and fortunately, C++ gives us the tools do that. But before that, lets make some of the terminology clear.
### 🔹 Bit Flags
Until now, we have mostly used fundamental data type variables to hold **single values**:
```cpp
int num{3};
// or
char letter{'A'};
// or
double pi{3.14159};
// etc.
```
However, instead of viewing objects as holding single values, we can instead consider each bit in an object as an independent Boolean value. When individual bits of an object are used as Boolean values, the bits are called **bit flags**. In other words, instead of one variable `==` one value, we can treat one variable `==` many tiny switches (bit flags).
#### Bit Flag Nomenclature
- A bit holding a `0`  is said to be **false**, **off**, or **not set**. 
- A bit holding a `1` is said to be **true**, **on**, or **set**.
- Also, when a bit is changed from a `0` to a `1`, or a `1` to a `0`, we say it has **set** or **cleared**.
- There are other terms, e.g., *flipped*, *inverted*, and many more, but they are directly linked to a method (member function) from `std::bitset`. We will cover those as we cover those methods specifically.
___
### 🔹 Using `std::bitset`
A **bitset** stores a fixed number of bits—each either `0` or `1`. You can think of it as an **array-like object of Boolean values**, optimized for space. It's not a real array, and it’s not dynamic like a vector—but it behaves similarly in some useful ways.

Here's the basic syntax:
```cpp
#include <bitset>

std::bitset<N> name{};
```
- Must include the bitset header - `#include <bitset>`
- `N` must be a non-negative integer, known at compile time (`size_t`).
- `name` is the identifier for your bitset object.

for example:
```cpp
std::bitset<8> myBitSet{0b10010101};
```
>*This creates a `std::bitset` that holds 8 bits, initialized with the binary value `10010101`*.

Even though we haven’t covered classes yet (see: [[Classes and Objects(STUB)]]), you can treat this `std::bitset<8>` type kind of like a custom-built container—similar to how `int` is a type, or how `std::vector<int>` will be later.
#### Bit Position
You may refer to [[Memory Management - Basics]] for more details, but in short:
```text
7 6 5 4 3 2 1 0 : Bit position 
1 0 0 0 1 0 1 0 : Bit Sequence 
```

To be crystal clear for `std::bitset`:
```cpp
std::bitset<8> bin{0b10001010};

bin[7] == bin 7 == 128's place == 1
bin[6] == bin 6 == 64's  place == 0
bin[5] == bin 5 == 32's  place == 0
bin[4] == bin 4 == 16's  place == 0
bin[3] == bin 3 ==  8's  place == 1
bin[2] == bin 2 ==  4's  place == 0
bin[1] == bin 1 ==  2's  place == 1
bin[0] == bin 0 ==  1's  place == 0
```
### 🔹 Why it feels "array-like"
Well as you can see so far, to access and modify individual bits using the subscript operator:
```cpp
myBitSet[1] = 1;
myBitSet[7] = 0;
```
This looks just like modifying an array, and that’s no accident. `bitset` is designed to be intuitive to use—but under the hood, it packs bits tightly together, saving memory and allowing for efficient bitwise operations.
Another array-like trait: the size is **fixed**. You can’t resize a `bitset` at runtime, just like you can’t resize a raw array.
### 🔹 Member Functions
`std::bitset` provides 4 key member functions that really round the toolset out. Each of these member functions takes the bit position as an argument:
1. `.test()`: Allows us to query whether a bit is *on* or *off* (`1` or `0`).
2. `.set()`: Allows us to turn a bit *on* (will do nothing if bit is already on).
3. `.reset()`: Allows us to turn a bit *off* (will do nothing if bit is already off).
4. `.flip()`: Allows us to *flip* a bit value from `0` to `1`, or `1` to `0`.
___
### 📌 Key Definitions

___
### 🧠 Flashcards
