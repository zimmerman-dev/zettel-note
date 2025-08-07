#### 📝 Note: Loops - Nesting 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚7:02 pm  📆 Tue Aug 5
 🔗 **Related Concepts**: #cpp #note [[Boolean Logic]] , [[Conditionals]] , [[Increment and Decrement]] , [[Statements and Expressions]] , [[Control Flow]] , [[Loops]] , [[Loops - For]]
___
## ➰ Nested Loops

A nested loop is simply a loop placed inside of a loop. For this note, we will only consider nested `for` loops.

```cpp
for (initialization; condition; increment) {
	for (initialization; condition; increment) {
		// inner statement
	}
	// outer statement
}
```

#### Basics:
- The **outer loop** controls the overall iterations.
- For **each** iteration of the outer loop, the **inner loop** runs through all it's iterations
- This creates a layered, *grid-like* iteration pattern.
- The inner loop fully completes before the outer loop increments.

---

## 🔁 Nested Loop Flow

Iteration flow for nested `for` loops example:

```cpp
for (int i {1}; i <= 2; ++i) {        // <--> Outer Loop
	for (int j {1}; j <= 3; ++j) {    // <--> Inner Loop (body of outer loop)
		std::cout << i << "," << j << std::endl;  // <--> (body of inner loop)
	}
	std::cout << std::endl;
}
```

#### 🌊 Flow Breakdown:

1. **Outer loop begins**
   - `i` is initialized to `1`.
   - Condition `i <= 2` is `true` ➡️ **enter outer loop**
   - **Inner loop starts**
     - `j = 1`, condition `j <= 3` is `true` ➡️ print `(1,1)`
     - `j` increments → `2`, condition `true` ➡️ print `(1,2)`
     - `j` increments → `3`, condition `true` ➡️ print `(1,3)`
     - `j` increments → `4`, condition `false` ❌ **inner loop ends**

2. **Outer loop continues**
   - Executes any code after inner loop (`endl`)
   - `i` increments → `2`, condition `true` ➡️ **enter outer loop again**
   - **Inner loop restarts**
     - `j` runs through same sequence → prints `(2,1) (2,2) (2,3)`  
     - ❌ **inner loop ends**

3. **Outer loop final check**
   - `i` increments → `3`, condition `false` ❌ **outer loop ends**
   - Program continues with code after the loops (if any).

---
#### 🔢 **Arrays & Vectors**

You can use nested loops to process a 1D array multiple times or compare elements.
#### ✅ Example: Comparing every element with every other

```cpp
int arr[3] {10, 20, 30};

for (int i = 0; i < 3; ++i) {
	for (int j = 0; j < 3; ++j) {
	    std::cout << arr[i] << " - " << arr[j] << std::endl;
	} 
}
```

In this example, there’s **only one array** (`arr`), but we have **two loops**:
- `i` is the outer index, selecting one element of `arr` at a time.
- `j` is the inner index, iterating over the same set of elements of `arr`.
##### Key difference between Arrays and Vectors

The logic is identical to arrays, but you use `.size()` instead of a hardcoded length.

###  🔢 **2D Vectors and Arrays**

With **2D structures**, the outer loop goes through **rows**, and the inner loop goes through **columns**.
#### ✅ Example: Printing a 2D Vector

```cpp
std::vector<std::vector<int>> matrix {
	{1, 2, 3}, {4, 5, 6}
};
for (size_t i = 0; i < matrix.size(); ++i) {
	for (size_t j = 0; j < matrix.at(i).size(); ++j) {
		std::cout << matrix.at(i).at(j) << " ";
	}
}
```

Member functions present:
- `matrix.size()` - Number of inner vectors (rows).
  - Ex: `matrix.size() = 2`
- `matrix.at(i)` - Accesses the *i-th row vector*.
  - Ex: `matrix.at(0) = {1, 2, 3}`
- `matrix.at(i).size()` - Returns the number of elements in row `i`.
  - Ex: `matrix.at(0).size() = 3`
- `matrix.at(i).at(j)` - Accesses the element at row `i`, column `j`.
  - Ex: `matrix.at(0).at(0) = 1`
  - Ex: `matrix.at(0).at(1) = 2`
  - Ex: `matrix.at(0).at(2) = 3`
  - Ex: `matrix.at(1).at(0) = 4`
  - Ex: `matrix.at(1).at(1) = 5`
  - Ex: `matrix.at(1).at(2) = 6`

*`size_t` is often used for loop indices because it matches the type returned by `.size()`. Also, the fact that it's unsigned means negative indices don't make sense. See [[climits | size_t and limits]] for more details.*

---
#### 🌩️ **Jagged Arrays**

Inner vectors can have **different sizes**.

```cpp
for (size_t i = 0; i < jagged.size(); ++i) {      // outer: 3 rows
    for (size_t j = 0; j < jagged.at(i).size(); ++j) { // This saying: “Only loop as far as the number of elements **in this specific row `i`**.”
        std::cout << jagged.at(i).at(j) << " ";
    }
}
```

- **Outer i = 0** → inner runs `j < 2` (because row 0 has 2 elements)
- **Outer i = 1** → inner runs `j < 3` (because row 1 has 3 elements)
- **Outer i = 2** → inner runs `j < 1` (because row 2 has 1 element)

If you had used `jagged.size()` instead, the inner loop would always think there are **3 elements** and crash when `i = 2`.

#### ✅ **In short:**

- `jagged.size()` → **number of rows** (outer dimension).
- `jagged.at(i).size()` → **number of columns in row i** (inner dimension).
- This distinction matters **only for jagged structures**—in a perfectly rectangular 2D array, both would effectively be constant per row.
- This structure is common when rows naturally differ in length (e.g., triangle patterns, adjacency lists in graphs, etc.).

### `matrix[i].size()` vs. `matrix.at(i).size()`

|     Access Style      |                                                         Safety                                                         |                            Performance                             |                                                      When to Use                                                       |
| :-------------------: | :--------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------: | :--------------------------------------------------------------------------------------------------------------------: |
|  `matrix[i].size()`   |   **No bounds checking** → if `i` is out of range, it causes **undefined behavior** (could crash or corrupt memory).   | Slightly **faster**, because it doesn’t perform any safety checks. | Commonly used in **performance-critical** code where you’re sure indexes are valid (e.g., graphics, game loops, etc.). |
| `matrix.at(i).size()` | If `i` is invalid, it throws a `std::out_of_range` exception instead of corrupting memory due to runtime bounds checks |        Slightly **slower**, because it has to do the check.        |  Safer in cases where you’re not 100% sure your indexing is correct (e.g., user input, debugging, early development).  |
