#### 📝 Note: Variables and Constants 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:28 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #types  [[Data Types]] , [[Constants]]
___
#### What is a variable?
A variable is an abstraction for a memory location. It allows programmers to use meaningful names and not memory addresses.

>[!note] Variables have:
>- Type: integer, real number, string, etc., ...
>- Value: the contents i.e. 1, 10.2, "string", etc., ...

#### Variables must be declared before used:

>[!info] Rules for Variable naming:
> - Can contain letters, numbers, and underscores. Case sensitive.
> - Must begin with a letter or underscore (cannot begin with a number).
> - Cannot use C++ reserved keywords.
> - Cannot redeclare a name in the same scope 

>[!info] Best Practices:
> - Be consistent with your naming conventions. 
> - Use meaningful names.
> - Never use a variable before initializing them.
> - Declare variables close to when you need them in your code.

##### Initializing Variables

```cpp title:Variables
int age;        // Unitialized

int age = 21;   // C-like initialization

int age (21);   // Constructor initialization

int age {21};   // C++11 list initialization syntax
```

___

>[!info] 'Global' and 'Local' Variables
>- Up to this point we have been, we've declared our variables within the curly braces of the main function. This is what's known as a *local variable* because their scope or visibility is limited to statements within the main function.
> - Variables declared outside of any function are called *global variables.* Unlike local variables, global variables are automatically initialized to zero.
