 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚8:17 pm  📆 Sun Sep 7
 🔗 **Related Concepts**: #note #cpp
___
## 📝 Note: Arithmetic Conversions(STUB)

### Example of arthmetic conversion between signed and unsigned ints

2. Here is another example of where things can go wrong:
```cpp
#include <iostream>

// assume int is 4 bytes
int main()
{
    signed int s { -1 };
    unsigned int u { 1 };

    if (s < u) // -1 is implicitly converted to 4294967295, and 4294967295 < 1 is false
        std::cout << "-1 is less than 1\n";
    else
        std::cout << "1 is less than -1\n"; // this statement executes

    return 0;
}
```




























___
### 📌 Key Definitions










___
### 🧠 Flashcards

