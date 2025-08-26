 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:04 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #note #cpp[[Data Types]], [[Sizeof]], [[Functions - Passing Arrays & Vectors]], [[Vectors]]
___
## 📝 Note: Arrays
### Syntax
```cpp
Element_Type array_name [constant number of elements] = { value1, value2, ...};
```
### What is an array?
- A **compound data structure** — a fixed-size collection of elements.
- All elements are of the **same type** and stored in **contiguous memory locations**.
- Each element can be **accessed directly** by its index.

---
### Array Declaration Styles
```cpp title:Declarations
int nums[5];               // Uninitialized — contains garbage
int nums[3] = {};          // All elements zero-initialized
int nums[] = {1, 2, 3, 4}; // Size inferred from initializer
```
---
### Why use arrays?
Arrays let you group related data under a single name, instead of declaring many individual variables.

```cpp title:Syntax
// Without array:
std::string car1 = "Volvo";
std::string car2 = "Ford";
std::string car3 = "BMW";
std::string car4 = "Chrysler";

// With array:
std::string cars[4] = {"Volvo", "Ford", "BMW", "Chrysler"};
```
---
### Indexing and Access
Arrays are **zero-indexed**, meaning the first element is at index `0`. The last element's index in an array is always `-1`.

```cpp title:Access
std::cout << cars[0]; // Volvo
std::cout << cars[1]; // Ford
std::cout << cars[2]; // BMW
std::cout << cars[3]; // Chrysler
```
>So for `cars[4]`, valid indices are `0` to `3`
---
### Access cont'd
Think of an array like a row of labelled boxes:

```cpp title:Index
// Index:     0        1         2         3
// Value:  "Volvo"   "Ford"    "BMW"   "Chrysler"
```

Want to change `"Ford"` to `"Toyota"`?
```cpp
cars[1] = "Toyota"; // Overwrites element at index 1
```
You can:
- **Read** an element: `std::string x = cars[2];`
- **Write** to an element: `cars[0] = "Honda";`
---
### Array Rules (C++)
- The **size** of a raw array must be known at **compile time**.
  - Cannot be based on user input or runtime values.
  - Must use a compile-time constant (e.g., `const int size = 5;`).
- Arrays are **static**: once created, you cannot grow or shrink them.
- **Out-of-bounds access is undefined behavior.**

  ```cpp
  std::cout << cars[4]; // ❌ No bounds checking in raw arrays
  ```
---
### If you need dynamic sizing...
Use `std::vector`.

Vectors behave like flexible arrays:
- Grow/shrink at runtime
- Handle memory management automatically
- Safer and more feature-rich
#### See: [[Vectors]]
---
### 📌 Key Definitions
1. **Array**: A compound data structure that is fixed in size, that holds a sequence of same type elements contiguously in memory. 
2. **Element**: A single value inside an array, accessed by its index.
3. **Index**: The position of an element in the array, e.g., arr[0], arr[1], arr[2], …, arr[i].
4. **Zero-index**: Array indexing in C++ always starts at 0.
5. **Array Name**: Acts as a label for the entire sequence; in most expressions, it decays into a pointer to the first element.
6. **Contiguous Memory**: A single, unbroken block of addresses in memory. All bytes are laid out back-to-back in order with no gaps or fragmentation.
7. **Array Size**: The number of elements in a built-in array is fixed at compile time and must be defined when the array is created.
8. **Decay to Pointer**: When used in most expressions, an array name evaluates (decays) to the address of its first element.
9. **Out-of-Bounds Access**: Accessing an element outside the valid range of an array is undefined behavior (UB).


---
### 🧠 Flashcards

- What is an array?|||A fixed-size, contiguous sequence of elements of the same type stored under one name. #flashcards
<!--SR:!2025-08-28,3,269-->

- What is an array element?|||A single value inside an array, accessed using its index. #flashcards
<!--SR:!2025-08-28,3,269-->

- What is an index in an array?|||The position of an element relative to the start of the array; starts at `0` in C++. #flashcards
<!--SR:!2025-08-27,2,249-->

- What is zero-indexing?|||The convention where the first element of a sequence is always at index `0`. #flashcards
<!--SR:!2025-08-28,3,269-->

- What happens if you access an array index outside its size?|||It’s undefined behavior (UB). There is no automatic bounds checking for raw arrays. #flashcards
<!--SR:!2025-08-27,2,249-->

- How are arrays stored in memory?|||As a single, contiguous block of memory where elements are laid out back-to-back with no gaps. #flashcards
<!--SR:!2025-08-28,3,269-->

- What does it mean when an array “decays” to a pointer?|||In most expressions, the array name evaluates to the address of its first element. #flashcards
<!--SR:!2025-08-26,1,229-->

- Does an array variable always decay to a pointer?|||No. It does **not** decay when used with `sizeof`, `&array`, or in template argument deduction. #flashcards
<!--SR:!2025-08-27,2,249-->

- The size of a built-in array must be known at ==compile time==. #flashcards
<!--SR:!2025-08-28,3,269-->

- True or False, the size of a built-in array cannot change after creation? ==true== #flashcards
<!--SR:!2025-08-28,3,269-->

- To zero-initialize an array, you use ==empty curly braces== during initialization. #flashcards
<!--SR:!2025-08-28,3,269-->

- Use a ==std::vector== when you need a dynamic, resizable container. #flashcards
<!--SR:!2025-08-28,3,269-->

- Use a ==raw array== when the size is fixed and known at compile time. #flashcards
<!--SR:!2025-08-28,3,269-->

- Unlike raw arrays, vectors handle ==memory management== automatically. #flashcards
<!--SR:!2025-08-28,3,269-->

- Unlike raw arrays, vectors provide built-in ==bounds== checks. #flashcards
<!--SR:!2025-08-28,3,269-->

