#### 📝 Note: Arrays 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:04 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #types [[C++ Headers Index]] , [[Vectors]] , [[C++ Syntax Reference]]
___
## 🧮 Arrays (C++)

### Syntax

`Element_Type array_name` `[constant number of elements]` `=` `{ value1, value2, ...};`

### What is an array?

- A **compound data structure** — a fixed-size collection of elements.
- All elements are of the **same type**.
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

Arrays are **zero-indexed**, meaning the first element is at index `0`. The last element in an array is always `-1`.

```cpp title:Access
std::cout << cars[0]; // Volvo
std::cout << cars[1]; // Ford
std::cout << cars[2]; // BMW
std::cout << cars[3]; // Chrysler
```

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
  - Must use a constant expression (e.g., `const int size = 5;`).
- Arrays are **static**: once created, you cannot grow or shrink them.
- **Out-of-bounds access is undefined behavior.**
  ```cpp title:Out-of-bounds
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