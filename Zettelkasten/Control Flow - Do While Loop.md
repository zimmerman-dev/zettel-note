♻️ (*MinGW, Windows11, Codelite*)   
 ⌚11:24 pm  📆 Sat Aug 2
 🔗 **Related Concepts**: #cpp #note  [[Control Flow - Loops Overview]]
___
## 📝 Note: Loops - Do While 

```cpp
do {
	statements;
} while (expression);
```    
### 🔹 **How It Works**
1. Execute the statements inside the loop.
2. Evaluate the condition.
3.  If `true`, go back to step 1.
4. If `false`, exit the loop.

This is why `do-while` loops always execute **at least once**, even if the condition starts off false.
### 🔹 **Example 1:** Input Validation
```cpp
int number {};
do {
	std::cout << "Enter an int between 1 and 5: ";
	std::cin >> number;
	
} while (number < 1 || number > 5);
std::cout << "Thanks";
```
### 🔹 **Example 2:** Menu System
```cpp
int choice {};
std::cout << "Welcome! Pick from the following choices below.\n";

do {
	std::cout << "Choice [1]\n";
	std::cout << "Choice [2]\n";
	std::cout << "Quit [3]\n";
	std::cin >> choice;
} while (choice != 3);
std::cout << "Exiting Program...\n";
return 0;
```
### 🔹 **Example 3:** Menu System (User driven continuation)
```cpp
char selection {};

do {
	double width {}, height {};
	std::cout << "Enter a the width then height separated with a space: ";
	std::cin >> width >> height;

	double area {width * height};
	std::cout << "The area is " << area << std::endl;
	std::cout << "Calculate another? [Y]es: ";
	std::cin >> selection;
} while (selection == 'Y' || selection == 'y');
std::cout << "Come back soon!";
```
### 🔹 **Example 4:** Iterating Through Vector
```cpp
std::vector<char> vowels {'a', 'e', 'i', 'o', 'u'};
int i {};

if (!vowels.empty()) {
	do {
	std::cout << vowels[i] << std::endl;
	++i;
	} while (i < vowels.size());
}
```
note:  “If the vector is empty, `do-while` would access an invalid index, so guard with `!vowels.empty()` when needed.”

---
### 🔹 **When to Use**
Use a `do-while` loop when you want a block of code to execute **at least once**, and then **repeat only while** a certain condition remains true.

- ✅ When the **first iteration must always run**, regardless of the condition
- ✅ Menu systems where the menu should display at least once
- ✅ Input prompts where the user should be asked at least once before validation
- ✅ Retry mechanisms where the action should attempt first, then check for continuation
### 🔹 **Key Difference from `while`**
While the `while` loop is a pre-test loop, a `do while` loop is a post-test loop meaning that the **condition is evaluated after** the loop body runs once. Therefore, the loop body **always executes at least once**, even if the condition is false initially.