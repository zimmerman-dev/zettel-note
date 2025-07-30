#### 📝 Note: Iostream 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:22 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #preprocessor [[C++ Headers Index]] 
___
### C++ iostream Library (Standard Input/Output Streams)

>[!<iostream>]
>The iostream library provides objects which can read user input and output data to the console or to a file.


| Object    | Description                                                                          |
| --------- | ------------------------------------------------------------------------------------ |
| **cerr**  | An output stream for error messages.                                                 |
| **clog**  | An output stream to log program information.                                         |
| **cin**   | An input stream that reads keyboard input from the console by default.               |
| **cout**  | An output stream which writes output to the console by default.                      |
| **wcerr** | The same as **cerr** but outputs wide char (*wchar_t*) data rather than *char* data. |
| **wclog** | The same as **clog** but outputs wide char (*wchar_t*) data rather than *char* data. |
| **wcin**  | The same as **cin** but interprets each input character as a wide char (*wchar_t*).  |
| **wcout** | The same as **cout** but outputs wide char (*wchar_t*)                               |

```cpp title:cout/cin
#include <iostream>
#include <string>

int main() {

	 std::string name; 
	
	std::cout << "Hello! Enter your name: "; // console output
	std::cin >> name;

	std::cout << "Hello, " << name << std::endl;
	return 0;
}
```

> [!Caveat for code above:]
> When using only std::cout and std::cin along with with the string library, cin will only save what the user types in until white space. With that in mind, if you go and type in "(first name) + (last name)", it's only going to save up to the first bit of white space, meaning it will omit a last name if the user types that in as well.

