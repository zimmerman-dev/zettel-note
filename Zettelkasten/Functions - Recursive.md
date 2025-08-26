#### 📝 Note: Functions - Recursive 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚1:48 am  📆 Sat Aug 23
 🔗 **Related Concepts**: #note #cpp
___
```cpp  
/* Recursion Notes  
*
* The Five-Rule Checklist
* 1. Base Case: The smallest input you can answer without recursion. 
* 
* 2. Progress: Make the input smaller (closer to base) every call. 
*
* 3. Recursive Call: Assume it works and returns the right answer. 
*
* 4. Combine: Use that returned answer to build this level's answer. 
*
* 5. No Side Quests: Avoid extra work after the recursive call unless * it's part of the combine step. 
* 
* 
*/
#include <iostream> 
  
int factorial(int n) {  
    if (n == 0 || n == 1)  
        return 1;  
    return n * factorial(n - 1);  
}  
  
int main() {  
   std::cout << factorial(3);  
    return 0;  
}
```
