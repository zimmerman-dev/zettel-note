#### 📝 Note: Loops - Do While 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚11:24 pm  📆 Sat Aug 2
 🔗 **Related Concepts**: [[Boolean Logic]] , [[Conditionals]] , [[Increment and Decrement]] , [[Statements and Expressions]] , [[Control Flow]] , [[Loops]]
___
## ➰ `Do While` **Loop**
While the `while` loop is a pre-test loop, a `do while` loop is a post-test loop meaning that the **condition is evaluated after** the the loop body runs once. Therefore, the loop body **always executes at least once**, even if the condition is false initially.

```cpp
do {
	statements;
} while (expression);
```    

#### **How It Works**
1. Execute the statements inside the loop.
2. Evaluate the condition.
3.  If `true`, go back to step 1.
4. If `false`, exit the loop.

This is why `do-while` loops always execute **at least once**, even if the condition starts off false.


#### ✅ **Example 1:** Input Validation
```cpp
int number {};
do {
	std::cout << "Enter an int between 1 and 5: ";
	std::cin >> number;
	
} while (number <= 1 || number >= 5);
std::cout << "Thanks";
```


#### ✅ **Example 2:**
```cpp
```
In this example, the loop iterates 5 times, because the condition *remains*  true 'while' i is **less** than 5.  Logically, it prints `i` once, then iterates, checks the condition, and prints `i` again *while* the condition remains true.

#### ✅ **Example 3:**
```cpp
```


>[!note] Note on `++i` vs. `i++`:
>- `++i` (prefix) increments `i` **before** its value is used in an expression.
>- `i++` (postfix) increments `i` **after** its value is used in an expression.
>- Here, because the increment is a standalone statement, there’s no difference in behavior.

#### ✅ **Example 4:** Arrays
```cpp
int scores [] {100,90,80};
int i {0};

while (i < 3) {
	std::cout << scores[i] << std::endl;
	++i;
}
```
In this example, the loop continues **as long as** `i` is less than `3` (the number of elements in the array). `scores[i]` retrieves the element at index `i` and prints it. `++i` increments `i` by 1, moving to the next element for the next iteration.

**Iteration Flow**
- **Iteration 1**: `i = 0`, prints `scores[0]` → 100
- **Iteration 2**: `i = 1`, prints `scores[1]` → 90
- **Iteration 3**: `i = 2`, prints `scores[2]` → 80 
- After this, `i` becomes `3`, the condition `i < 3` fails, and the loop exits.

#### ✅ **Example 5:** Input Validation
```cpp
int number {};

std::cout << "Enter an integer less than 100: ";
std::cin >> number;

while (number >= 100) {
std::cout << "Enter an integer LESS than 100: ";
std::cin >> number;
}

std::cout << "Thanks!";
```
In this example, the program asks for an integer. *if* the user enters an integer 100 or more, the condition is `true` so it asks again. The loop continues until the user enters a valid number.

#### ✅ **Example 6:** Input Validation - Bool Flag
```cpp
bool done {false};
int number {0};

while (!done) {
	std::cout << "Pick a number greater than 1, but less than 5: ";
	std::cin >> number;
	if (number <= 1 || number >= 5)
		std::cout << "Out of range, try again\n";
	else {
	std::cout << "Thanks!" << std::endl;
	done = true;
	}
}
```
n this example, a **Boolean flag** (`done`) controls the `while` loop. The loop continues running as long as `done` is `false`. Each iteration, the program asks for user input and checks if it falls within the valid range. If the input is invalid, it prompts the user again. When the input is valid, the program sets `done` to `true`, causing the loop to terminate.

#### Difference?: 
The first input validation uses the loop condition directly, while the second uses a Boolean flag to explicitly control when to exit.

#### 📝 **When to Use**
Use a `while` loop when you want a block of code to keep executing **as long as** a certain condition remains true. 

- ✅ Input validation 
- ✅ Waiting for events
- ✅ repeating actions until a stop condition occurs.



#### ✅ **Key Difference from `for`**

- `for` puts **initialization**, **condition**, and **increment** neatly at the top.

- `while` only handles the condition—you control everything else explicitly.

This makes `while` **better for loops where you don’t know how many iterations are needed** (e.g., reading input until EOF).