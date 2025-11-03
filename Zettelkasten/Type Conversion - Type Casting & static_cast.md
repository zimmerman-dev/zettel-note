♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:28 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #note #cpp [[Fundamental Data Types]], [[Functions - Parameters & Arguments]], [[Type Conversion - Overview]] , [[Type Conversion - Implicit Type Conversion]]
___
## 📝 Note: Type Conversion - Type Casting & static_cast
When you *manually* tell the compiler: ==*“Hey — treat this value as if it's a different type,”*==  that’s called **explicit type casting**.

C++ gives you two ways to do this:
### 🔹Preferred: `static_cast`
```cpp
static_cast<type>(value)
```
- Used for converting between compatible numeric types (e.g. `int → double`)
- Compile-time checked — **safer than C-style**
##### Example:
```cpp 
#include <iostream>

int main() {
int total {};
int num1 {}, num2 {}, num3 {};
const int count {3};

std::cout << "Enter three ints separated by spaces: ";
std::cin >> num1 >> num2 >> num3;

total = num1 + num2 + num3;

double average {0.0};

average = static_cast<double>(total)/count;

std::cout << "The average of your ints are: " << average << std::endl;
return 0;
}
```
> 🧠 _If you didn’t cast `total` to `double`, integer division would occur and the result would be wrong (truncated)._
### 🔹Avoid C-style Cast
```cpp
(type)value
```
- Works, but harder to read and easier to misuse
- Modern C++ encourages `static_cast` instead
