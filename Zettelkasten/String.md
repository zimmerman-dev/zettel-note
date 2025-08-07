#### 📝 Note: String 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:27 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #cpp #note [[C++ Headers Index]] , [[Variables and Constants]] , [[C++ Syntax Reference]]
___

## 🏛️ C-Style Strings

A string in C is a sequence of characters that is stored in uninterrupted block of memory. They are implemented as an array of characters, terminated by a *null character*. This is why they are referred to as a null-terminated string in C/C++.

### 🌀 String Literal

An example of a string literal is what we have so far been using for our `std::cout` statements--it's a sequence of characters in double quotes, e.g., `"StringLiteral"`
- constant - meaning they are unchanging like a integer literal.
- terminated with null character

Example of string literal and how its stored in memory:

String: "C++ is fun!"

|  0  |  1  |  2  |  3  |  4  |  5  |  6  |  7  |  8  |  9  | 10  |   11   |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :----: |
|  J  |  o  |  h  |  n  |     |  B  |  i  |  s  |  h  |  o  |  p  | \0 |

This string has exactly 11 characters, but the compiler allocates 12 character because it need space for the null terminator at the end. With that in mind, another way to look at this is:

`char myName[] {"John Bishop"};`

With this example we can see how a string in C is just an array, where the first character is indexed to 0. The reason for the null terminator is to act as a "sentinel value", marking the end of the sequence within the allocated memory. This allows it to know when to end processing when \0 is encountered

**Problems:**
With C-style strings that are just arrays, they also inherent it's static behavior, meaning that if you try to access it and a character, it would cause problems due to their (arrays) fixed nature.

Declaring variables:

Lets take this example:
```cpp
char myName[8] {"Frank"};
myName[5] = 'y'; // OK
```

| 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| F   | r   | a   | n   | k   | (y) | \0  | \0  |
Again, this is just an array, so we can see how this would work because we have declared the array to have three null characters in this array.

[[cstring]] 

`char str[80];`

- `strcpy(str, "Hello ");`   // Copy
- `strcat(str, "there");`     // Concatenate
- `cout << strlen(str);`       // 11
- `strcmp(str, "Another");` // > 0




## ✅ What I Know So Far

- What is a `std::string`?
- How have I used it in code?
- Any methods or functions I’ve learned?

---

## 🛠 Things I’ve Done with Strings

- Concatenation examples?
- Input/output?
- Accessing characters?
- String length?
- Substrings?

---

## ❓Open Questions

- What’s the difference between `std::string` and C-style strings?
- Have I seen `std::string_view`? What’s it for?

---

## 🧱 Future Topics to Explore

- Unicode/encodings?
- Conversion between string types?
- Performance and memory?