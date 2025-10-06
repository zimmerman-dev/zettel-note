 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚12:58 pm  📆 Sat Oct 4
 🔗 **Related Concepts**: #note #cpp [[Bit Manipulation - Overview]] . [[Operators - Bitwise Operators & Bit Manipulation]] , [[Binary Numbers - Overview]] , [[Memory Management - Overview]]
___
## 📝 Note: Bit Manipulation - Bit Masks
In the last few modules, we learned the basic of bit manipulation using `std::bitset<size_t N>`, and regular old bitwise operators. Lets go from theory and fundamentals, and move into how bit manipulation is commonly done.
### 🔹 Bit Masks
As we know, to manipulate bits (e.g., turn them on/off), we need some way to identify the bits individually. Unfortunately, **bitwise operators don't work on specific bit positions—they work on bit masks**. 

A **bit mask** is a predefined set of bits that is used to to select which specific bits will be modified by subsequent operations. In practice, their purpose is to block the bitwise operators from *touching* bits we don't want modified, and allows access to the ones we *do want* modified.
#### Defining bit masks
The simplest set of bit masks to define one bit mask for each bit position. We use `0`'s to mask out bits we don't want *touched*.
```cpp
#include <cstdint>

constexpr std::uint8_t mask0{0b0000'0001};
constexpr std::uint8_t mask1{0b0000'0010};
constexpr std::uint8_t mask2{0b0000'0100};
constexpr std::uint8_t mask3{0b0000'1000};
constexpr std::uint8_t mask4{0b0001'0000};
constexpr std::uint8_t mask5{0b0010'0000};
constexpr std::uint8_t mask6{0b0100'0000};
constexpr std::uint8_t mask7{0b1000'0000};
```
___
### 🧠 Flashcards
