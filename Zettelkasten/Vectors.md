#### 📝 Note: Vectors 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:28 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #cpp #note [[C++ Headers Index]] , [[Arrays]] , [[Standard Template Library]] , [[C++ Syntax Reference]] 
___
## 🔢 Vectors (C++)

A vector is an *class template* container defined in the **Standard Template Library (STL)**. 
* You must include the `<vector>` header.
* It belongs to the `std` namespace.
### Syntax

`std::vector<element_type>` `vector_name;`

---
### What is a vector?

- **A compound data structure** — a dynamically sized collection of elements.
- All elements are of the **same type**, stored contiguously in memory.
- Each element can be **accessed directly** by index.

>[!note] Vector vs. Arrays
>- Vectors can grow and shrink at runtime.
>- Vectors support **array-like syntax** but offer more functionality.
>- Vectors provide tools like `.sort()` , `.reverse()` , `.find()`  , etc.
>- Vectors support **bounds-checked access** with `.at()`; arrays do not.

---
### Vector Declaration Styles

```cpp title:Declarations
std::vector<char> vowels;
// Empty, clean – contains no elements

std::vector<char> vowels(5);
// 5 default-initialized chars: ['\0', '\0', '\0', '\0', '\0']

std::vector<char> vowels = {'a', 'e', 'i', 'o', 'u'};
// Initializer list – inserts those specific values

std::vector<int> tops(5, 3);
// Constructor: 5 elements, each set to 3 → [3, 3, 3, 3, 3]

std::vector<int> tops = {3, 3, 3, 3, 3};
// Initializer list: explicitly sets each value
```

---

### Indexing and Access

Accessing vector elements using **array syntax** (no bounds checking):

`vector_name[element_index];`

```cpp title:Access
std::vector<std::string> names {"tom", "jon", "joe", "bob", "jim"};

std::cout << names[0] << std::endl;
std::cout << names[1] << std::endl;
std::cout << names[2] << std::endl;
std::cout << names[3] << std::endl;
std::cout << names[4] << std::endl;
```


```cpp title:Index
// Index:     0        1         2         3          4
// Value:    tom      jon       joe       bob        jim
```

---
### Access cont'd - `.at()` 

Accessing vector elements (vector syntax):

`vector_name.at(element_index);`

```cpp title:.at(element_index)
std::vector<std::string> names {"tom", "jon", "joe", "bob", "jim"};

std::cout << names.at(0) << std::endl;
std::cout << names.at(1) << std::endl;
std::cout << names.at(2) << std::endl;
std::cout << names.at(3) << std::endl;
std::cout << names.at(4) << std::endl;
```

This provides bounds-checked access -- throws `std::out_of_range` if invalid.

>[!note] Overwrite
>Want to change *"jon"* to *"tim"*?
 >`names.at(1) = "tim"; // Overwrites element at index 1`
 >---------------------------------------------------
 > - You can:
 > 	- **Read** an element: `std::string x = names[2];`
 > 	- **Write** to an element: `names.at(1) = "tim";`

---

### Dynamic Growth - `.push_back()`

Adds an element to the end of the vector. Space is automatically managed.

`vector_name.push_back(element);`

```cpp title:.push_back(element)
std::vector<int> nums {1,2,3}; // Size is three

nums.push_back(4); // 1, 2, 3, 4
nums.push_back(5); // 1, 2, 3, 4, 5
```

---

### Memory - `.size()`

Returns the number of elements currently stored in the vector. 

`vector_name.size()`

```cpp title:.size(element)
std::vector<int> nums {1,2,3,4};

std::cout << nums.size() << std::endl; // 4
```

It does **not** return the allocated memory capacity, only the number of the elements present.

---

## 🟦 **2D Vectors in C++**

A **2D vector** is simply a `std::vector` where each element is another `std::vector`:

```cpp
std::vector<std::vector<type>> vector_name;
```

Essentially, A 2D vector is a **vector** of **vectors**. You can create individual vectors and add them to the **2D vector**, Like so:

```cpp
std::vector<int> vector1 {1, 2, 3};
std::vector<int> vector2 {4, 5, 6};

std::vector<std::vector<int>> vector2D {vector1, vector2};
```

**OR**

```cpp
std::vector<int> vector1 {1, 2, 3};
std::vector<int> vector2 {4, 5, 6};

std::vector<std::vector<int>> vector2D;
vector2D.push_back(vector1);
vector2D.push_back(vector2);
```

**OR** you can cleanly initialize your 2D vector directly:

```cpp
std::vector<std::vector<int>> vector2D {
	{1, 2, 3},
	{4, 5, 6}
};
```

### ✅ **Linear Mental Model**

Think of it as a **linear plot of points** where the points on the line are organized into **containers**. The common way to think of 2D vectors is with outer and inner vectors with rows and columns. In the linear mental model, we don't use those words as they don't represent the linear mental model.

 Here's a visualization:
 ![[2DVectorModel.png]]

### 🧠 Accessing a 2D Vector (Linear Mental Model)

Lets continue with the example above. 
```cpp
std::vector<std::vector<char>> letters {
    {'a', 'b'},         // index 0
    {'c', 'd', 'e'},    // index 1
    {'f'},              // index 2
    {'g', 'h', 'i'}     // index 3
};

```

To access one of those inner vectors, use:
```cpp
letters.at(i)
```

To access a specific element _within_ an inner vector, use:
```cpp
letters.at(i).at(j)
```

For example:
- `letters.at(0).at(1)` → `'b'`
- `letters.at(1).at(2)` → `'e'`
- `letters.at(2).at(0)` → `'f'`
- `letters.at(3).at(2)` → `'i'`

Each `.at(i)` moves linearly through the outer vector (like stepping through train cars), and each `.at(j)` moves linearly through the contents of that car.

**Unsafe but common:**
```cpp
letters[i];   
letters[i][j];
```

See [[Loops - Nesting]] for information on iterating through vectors and 2D vectors.

---

### Vector Rules (C++)

- Vectors must be declared with a single, specific element type.
- All elements are stored contiguously in memory (like arrays).
- Vectors are dynamically resizable -- they grow as needed.
- Elements can be accessed directly using `[]` or `.at()`.
- Use `.push_back()` to add elements to the end.
- Empty vectors contain no elements, not garbage.
- Vectors are part of the Standard Template Library -- include `<vector>` header, and use the `std::` namespace.