#### 📝 Note: Type Casting 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:28 am  📆 Wed Jul 23
 🔗 **Related Concepts**: [[Mixed-Type Expressions]] , [[Statements and Expressions]] , [[Standard Library Reference]] , [[Data Types]] , [[]]
___
### 💥 Type Casting

When you explicitly tell the compiler, "Treat this value as a different type," it's called **Explicit Type Casting**.
```cpp title:Syntax
static_cast<type>(value)
```

- `static_cast` is **safe** for well-defined conversions (e.g., numeric types.)

- avoid **c-style casts** i.e., `(type)value`

```cpp title:Example
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