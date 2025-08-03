#### 📝 Note: For 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚4:12 pm  📆 Sat Aug 2
 🔗 **Related Concepts**: [[Boolean Logic]] , [[Conditionals]] , [[Increment and Decrement]] , [[Statements and Expressions]] , [[Control Flow]] , [[Loops]]
___
## 🔹 `for` **Loop**
A traditional `for` loop is ideal when you need to iterate a **specific number of times** or require control over the loop variable.

```cpp
for (initialization; condition; increment) {
    statement;
}
```    

#### **How It Works**
1. **Initialization** – executes once, setting up the loop control variable.  
2. **Condition** – checked **before each iteration**.  
   - If `true`, the loop body executes.  
   - If `false`, the loop terminates.  
3. **Body** – the statements inside the braces run when the condition is true.  
4. **Increment/Decrement** – updates the loop variable, then returns to the condition check.


#### ✅ **Example**

```cpp
for (int i = 0; i < 5; i++) {
    std::cout << i << " ";
}
```
>Output:  `0 1 2 3 4`

- `i` starts at 0 (**initialization**)  
- The condition `i < 5` determines whether the loop continues  
- After each iteration, `i++` runs, and the cycle repeats until the condition is false  

#### 📝 **When to Use**
- ✅ Counting iterations  
- ✅ Iterating over a specific range or subset  
- ✅ When loop control (init, condition, update) should be explicit at the top  