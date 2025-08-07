#### 📝 Note: Sizeof 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:24 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #cpp #note [[climits]]  , [[cfloat]] , [[Data Types]] [[C++ Syntax Reference]]
___
### Syntax

`sizeof(type);`


>[!hint] *sizeof* operator
> The sizeof operator determines size in bytes of a type or variable. This operator gets its information from the [[climits]] and [[cfloat]] libraries.

___

```cpp title:sizeof
#include <iostream>
#include <climits>

int main() {
	std::cout << "Sizeof Information:" << std::endl;
	std::cout << "===============================" << std::endl;

	std::cout << "char: " << sizeof(char) << " bytes." << std::endl;
	std::cout << "int: " << sizeof(int) << " bytes." << std::endl;
	std::cout << "u int: " << sizeof(unsigned int) << " bytes." << std::endl;
	std::cout << "short: " << sizeof(short) << " bytes." << std::endl;
	std::cout << "long: " << sizeof(long) << " bytes." << std::endl;
	std::cout << "llong: " << sizeof(long long) << " bytes." << std::endl;
    
    std::cout << "================================" << std::endl;
    
    std::cout << "float: " << sizeof(float) << " bytes." << std::endl;
    std::cout << "double: " << sizeof(double) << " bytes." << std::endl;
    std::cout << "ldouble: " << sizeof(long double) << " bytes." << std::endl;
    
    std::cout << "================================" << std::endl;
    
    // below uses values defined the climits header
    
    std::cout << "Minimum Values:" << std::endl;
    std::cout << "char: " << CHAR_MIN << std::endl;
    std::cout << "int: " << INT_MIN << std::endl;
    std::cout << "short: " << SHRT_MIN << std::endl;
    std::cout << "long: " << LONG_MIN << std::endl;
    std::cout << "llong: " << LLONG_MIN << std::endl;
    
    std::cout << "=================================" << std::endl;
    
    std::cout << "Maximum Values" << std::endl;
    std::cout << "char: " << CHAR_MAX << std::endl;
    std::cout << "int: " << INT_MAX << std::endl;
    std::cout << "short: " << SHRT_MAX << std::endl;
    std::cout << "long: " << LONG_MAX << std::endl;
    std::cout << "llong: " << LLONG_MAX << std::endl;
    
    std::cout << "=================================" << std::endl;
    
    // Below shows how sizeof can be used with variable names.
    
    std::cout << "sizeof using variable names:" << std::endl;
    
    int age{21};
    std::cout << "age is " << sizeof(age) << " bytes." << std::endl;
    // OR
    std::cout << "age is " << sizeof age << " bytes." << std::endl;
    
    double wage{22.4};
    std::cout << "wage is " << sizeof(wage) << " bytes." << std::endl;
    //OR
    std::cout << "wage is " << sizeof wage << " bytes.";
	return 0;
}
```
