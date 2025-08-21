auto#### 📝 Note: Ranged-based For 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚4:13 pm  📆 Sat Aug 2
 🔗 **Related Concepts**: #note #cpp [[Vectors]], [[Loops - Overview]]

___
## 🔹 **Range-based `for` Loop**
A range-based `for` loop is a **modern C++ construct** that simplifies iterating directly over the elements of a container (arrays, vectors, strings, etc.).

```cpp
for (element_declaration: container) {
	statement;
}
```
#### **How It Works**
1. **Container** – must support iteration (e.g., array, vector, string, etc.).
2. **Element Declaration** – defines a variable representing the current element in the container.
3. On each iteration, the loop assigns the next element to this variable.
4. The loop continues until all elements have been processed.
#### ✅ **Example**
```cpp
std::vector<int> nums {1,2,3,4,5};   /*    Container                */
int sum {};                          /*    Accumulator for total    */

for (auto n : nums) {                
	sum += n;                        /*    'n' is the element variable                                              representing each value in 'nums'  */
	                                 
	                                 /*    Add the current element 'n' to the                                         running total 'sum'              */
}
std::cout << "Sum: " << sum << std::endl;
```
>Output: `Sum: 15`
##### 📝 **When to Use**
- ✅ When you want to visit every element in order  
- ✅ When the index is irrelevant  
- ✅ When readability matters  
- ✅ When using `const` or references to avoid copies  
##### ❌ **When Not to Use**
- When you need the element index  
- When you’re iterating over only a subset  
- When modifying the container structure during iteration  
- When working with certain C APIs where you need explicit indices or raw pointers