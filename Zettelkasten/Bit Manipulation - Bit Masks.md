 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚12:58 pm  📆 Sat Oct 4
 🔗 **Related Concepts**: #note #cpp [[Bit Manipulation - Overview]] . [[Operators - Bitwise Operators & Bit Manipulation]] , [[Binary Numbers - Overview]] , [[Memory Management - Overview]]
___
## 📝 Note: Bit Manipulation - Bit Masks
In the last few modules, we learned bit manipulation using `std::bitset<size_t N>`, and basic bitwise operators. Lets go from theory and fundamentals, and move into how bit manipulation is commonly done.
### 🔹 Bit Masks 
A **bit mask** is a predefined set of bits that is used to select which specific bits will be modified by subsequent operations. In practice, their purpose is to block the bitwise operators from *touching* bits we don't want modified, and allows access to the ones we *do want* modified.
#### Defining bit masks
Since we can use binary literals in C++14 and beyond, we will use `0`'s to mask out bits we don't want *touched*. Then, when you use a binary flag, you can use bitwise operators to touch the bits in the position where the `1` is.
```cpp
std::uint8_t flags{0b0000'0000}; 
std::uint8_t mask0{0b0000'0001};
```
 In this example above, `mask0` is the template for the bit in the 0 position for our `flags` object.
### Example
Let’s think of `flags` like a wooden shelf with 8 cubbies in a row, hanging on the wall. Each cubby can hold one apple. If all cubbies are full, you’ve got 8 apples (i.e., all bits are set). If they’re all empty, you’ve got none. Now imagine you have 8 wooden slats — each one the same size as the shelf, and each has **a single hole** cut out. The hole in each slat lines up with **one specific cubby only**.

- `mask0` has a hole over cubby 0: `0b0000'0001`
- `mask1` has a hole over cubby 1: `0b0000'0010`
- …and so on.

When you hold up one of these slats in front of the shelf, you can only access the cubby with the hole — **you can’t see or touch the others at all**. That’s what a bitmask does. It blocks out all other bits and gives you a clean, safe way to **peek at or change exactly one cubby (bit)** without disturbing the rest.
```cpp
#include <cstdint>
#include <iostream>

std::uint8_t shelf{0b0000'0000}; 

[[maybe_unused]] constexpr std::uint8_t cubby0{0b0000'0001};
[[maybe_unused]] constexpr std::uint8_t cubby1{0b0000'0010};
[[maybe_unused]] constexpr std::uint8_t cubby2{0b0000'0100};
[[maybe_unused]] constexpr std::uint8_t cubby3{0b0000'1000};
[[maybe_unused]] constexpr std::uint8_t cubby4{0b0001'0000};
[[maybe_unused]] constexpr std::uint8_t cubby5{0b0010'0000};
[[maybe_unused]] constexpr std::uint8_t cubby6{0b0100'0000};
[[maybe_unused]] constexpr std::uint8_t cubby7{0b1000'0000};
```

Now that we understand what bitmasks do, how can we utilize similar techniques like `std::bitset` uses, i.e., `.test()`, `.flip()`, etc.?
___
### 🔹 Testing a bit
 Remember in [[Operators - Bitwise Operators & Bit Manipulation#🔹 Bitwise AND `&`| The prior note]], we learned we could use the bitwise AND (`&`) to compare to operands to get a resulting bit pattern?
 ```cpp
 Operand 1 == 0b0000;
 // AND
 Operand 2 == 0b0001;
 Result    == 0b0000;
 ```

Well, we can do the same thing here, except now, replace `Operand 1` with `shelf`, and `Operand 2` with `cubby0`, and the bitmask/slat metaphor will reveal itself to us.
```cpp
shelf  == 0b0000'0000;
// AND
cubby0 == 0b0000'0001;
Result == 0b0000'0000;
```

Since an AND operation only returns `1` when _both_ bits are set, and `cubby0` already has a `1` in the right position, the result will be `0` if `shelf` doesn’t have that bit set. With that in mind, we can now write a condition like this:
```cpp
if (static_cast<bool>(shelf & cubby0)) {
	std::cout << "There's an apple in cubby 0!\n";
} else {
	std::cout << "No apples in cubby0...\n";
} 
```
___
### 🔹 Setting a bit
Let's think back to our [[Logic Gates#OR Gate ` `| truth tables]] and ask: what operator guarantees we can turn a bit _on_ without accidentally flipping any others? Since our bitmask already has the bit set in the right position, the answer is simple. The OR operator (`|`) ensures the bit will be set, and if it’s already set, it leaves it unchanged. Like before, we set up or comparison:

```cpp
shelf = shelf | cubby0;
```
#### Example:
```cpp
std::cout << "No apples in cubby0. Would you like to set it? [y]es or [n]o: ";
std::uint8_t query{};
std::cin >> query;

if (query == 'y') {
  shelf |= cubby0; // <--- Compound assignment
  std::cout << "Apple is set in cubby0 . Here's the shelf: " << '\n';
}
else 
  std::cout << "Okay, goodbye!\n";
```
___
### 🔹 Resetting a bit (clear)
Okay, so we have no successfully set a bit in our `shelf` object. What do we do to remove the bit? We don't have a specific operator for it, but we can invert our bitmask with a NOT operator, and then compare our bitmask and flag objects using a bitwise AND operator. It would look like this:
```cpp
shelf = shelf & ~cubby0
```

Breakdown:
```cpp
shelf  == 0b0000'0001
// AND
~cubby == 0b0000'1110
shelf  == 0b1111'1110
```
___
### 🔹 Flipping a bit
To toggle a bit, we use the XOR operator. Remember, with a bitwise XOR, the resulting bit will be `1` as long as the two operands are different. If they're the same, resulting bit will be `0`. With that in mind, we know that the bitmask is always `1`. So if the flag is `1`, the flag and bitmask match and it toggles off. If the flag is `0`, the flag and bitmask will not match and the it toggles on.
```cpp
shelf = shelf ^ cubby;
```

```cpp
shelf == 0b0000'0001;
// XOR 
cubby == 0b0000'0001;
shelf == 0b0000'0000;
```
___
### 🔹 Modifying multiple bit flags
Lets break down an interesting function of the bitwise OR operator. To do this we will use an example with two separate bit patterns. Now, lets say we want to represent the **intersection** of A and B within another pattern, Pattern C. By using the bitwise OR, we can essentially combine all the common bits.

**If**:
Pattern A: `0b0000'0111`
Pattern B: `0b0000'1000`
`=`
Pattern C: `0b0000'1111`

Why does this matter? Well, by combining those patterns we can use this pattern C as a impermanent hybrid bitmask that allows you to touch multiple bits from your flag object at one time. With that, we can do things like this:
```cpp
[[maybe_unused]] constexpr std::uint8_t cubby0{0b0000'0001};
// ..
[[maybe_unused]] constexpr std::uint8_t cubby7{0b1000'0000};

if (shelf & (cubby0 | cubby1 | cubby2))
	std::cout << "Nothing needed, all bits are set." << '\n';
else
	(shelf |= (cubby0 | cubby1 | cubby2));
	std::cout << "Bits have been set." << '\n';
```
___
###  🔹TL;DR Reference

| Operation | Operator | Effect                                   | Example             |
| --------- | -------- | ---------------------------------------- | ------------------- |
| Test      | `&`      | Check if bit is set                      | `if (flags & mask)` |
| Set       | \|       | Sets bit, if set, nothing changes        | `flags` \|`= mask`  |
| Clear     | `& ~`    | Turns bit off, if off, nothing changes   | `flags & ~mask`     |
| Flip      | `^`      | Flips bit from `1` to `0`, or `0` to `1` | `flags ^= mask`     |

___
### 🧠 Flashcards

What is a bit mask used for in bit manipulation? 
?|? 
A bit mask is a predefined bit pattern used to select which bits in another value will be modified or checked, blocking access to others.

---

How do you define a bit mask in C++ for the lowest bit?
?|?
Using a binary literal: `constexpr std::uint8_t mask0{0b0000'0001};`

---

Which operator is used to test whether a bit is set?
?|?
Bitwise AND (`&`). Example: `if (flags & mask)`

---

What does `shelf |= cubby0;` do in a bitmask example?
?|?
It sets the bit in the position of `cubby0` to 1 without changing other bits.

---

How can you clear a bit using a mask?
?|?
Invert the mask with bitwise NOT (`~`) and combine with AND: `flags &= ~mask;`

---

What does the XOR (`^`) operator do when used with a bit mask?
?|?
It toggles (flips) the bit at the mask’s position — turns 1→0 or 0→1.

---

Why does the bitwise OR operator work for setting bits safely?
?|?
Because OR only turns bits on; if a bit is already 1, it stays 1, preventing accidental flips.

---

What is the result of combining two bit patterns with OR?
?|?
It produces a union — all bits that are set in either pattern become set in the result.

---

How can you set multiple bits at once using bit masks?
?|?
Combine multiple masks with OR: `flags |= (mask0 | mask1 | mask2);`

---

Why must you cast `(flags & mask)` to `bool` when testing a bit in an `if` statement?
?|?
Because the result of the AND is a numeric value, not a Boolean; `static_cast<bool>` ensures the condition evaluates correctly.


#flashcards 