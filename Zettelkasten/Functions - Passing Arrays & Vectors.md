#### 📝 Note: Functions - Passing Arrays & Vectors 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚10:56 pm  📆 Wed Aug 20
 🔗 **Related Concepts**: #note #cpp [[Arrays]], [[Vectors]], [[Functions - Parameters & Arguments]], [[Functions - References & Pointers(STUB)]], [[Sizeof]]
___
### Passing Arrays to Functions
We can pass an array to a function by providing square brackets in the formal parameter description like this:
```cpp
void print_array(int nums[]); // ⚠️ Missing size info! The function has no idea how many elements to process. 
```
>The array elements are not copied!
##### **Remember**:
An array name **evaluates to an address, or a location** in memory. So instead of the elements being copied into the array, only the address of the first element is copied.
##### **What does that mean?** 
The function has no idea how many elements are in the array since all it knows is the location of the first element (the name of the array).
### How do you fix this problem?
To fix this, you must also pass the size of the array, so it knows how many times to iterate.
```cpp
void print_array(int nums[], size_t size) {
// ...
}
```
>Now that we have added the size of the array, we could easily add a for loop to iterate through that array.

```cpp
void print_array(int nums[], size_t size) {
	for (size_t i {0}; i < size; ++i) {
		std::cout << nums[i] << '\n';
		}
	}
	// main() ...
```
### Potential Caveats
Since we are passing the location of the array, a function can modify the actual array!
### 🔒 Preventing Modification with `const`
- We can tell the compiler that function parameters are const, which can help mitigate a problem where we don't want to modify the array.
```cpp
void print_array(const int nums[], size_t size) {
	for (size_t i = 0; i < size; ++i) {
		nums[i] = 0; // 🚫 Any attempt to modify elements will cause compiler error
		std::cout << nums[i];
		}
	}
```