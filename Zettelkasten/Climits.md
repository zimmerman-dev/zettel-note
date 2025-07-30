#### 📝 Note: Climits 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:07 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #preprocessor  [[C++ Headers Index]] , [[Data Types]] , [[C++ Syntax Reference]]
___
### Sizes of integral types

>[!info]
>This header defines constants with the limits of fundamental integral types for the specific system and compiler implementation used.
> - The limits for fundamental floating-point types are defined in [[Cfloat|<cfloat>]]
> - The limits for width-specific integral types and other typedef types are defined in [[cstdint|<cstdint>]]


| name       | expresses                                                    | possible value*                           |
| ---------- | ------------------------------------------------------------ | ----------------------------------------- |
| CHAR_BIT   | Number of bits in a *char* object (byte)                     | 8 or greater*                             |
| SCHAR_MIN  | Minimum value for an object of type *signed char*            | -127 (-2^7+1) or less*                    |
| SCHAR_MAX  | Maximum value for an object of type *signed char*            | 127 (2^7-1) or greater*                   |
| UCHAR_MAX  | Maximum value for an object of type *unsigned char*          | 255 (2^8-1) or greater*                   |
| CHAR_MIN   | Minimum value for an object of type *char*                   | either SCHAR_MIN or 0                     |
| CHAR_MAX   | Maximum value for an object of type *char*                   | either SCHAR_MAX or UCHAR_MAX             |
| MB_LEN_MAX | Maximum number of bytes in multi character, for any locale   | 1 or greater*                             |
| SHRT_MIN   | Minimum value for an object of type *short int*              | -32767 (-2^15+1) or less*                 |
| SHRT_MAX   | Maximum value for an object of type *short int*              | 32767 (2^15-1) or greater*                |
| USHRT_MAX  | Maximum value for an object of type *unsigned short int*     | 65535 (2^16-1) or greater*                |
| INT_MIN    | Minimum value for an object of type * int*                   | -32767 (-2^15+1) or less*                 |
| INT_MAX    | Maximum value for an object of type *int*                    | 32767 (2^15-1) or greater*                |
| UINT_MAX   | Maximum value for an object of type *unsigned int*           | 65535 (2^16-1) or greater*                |
| LONG_MIN   | Minimum value for and object of type *long int*              | -2147483647 (-2^31+1) or less*            |
| LONG_MAX   | Maximum value for an object of type *long int*               | 2147483647 (2^31-1) or greater*           |
| ULONG_MAX  | Maximum value for an object of type *unsigned long int*      | 4294967295 (2^32-1) or greater*           |
| LLONG_MIN  | Minimum value for an object of type *long long int*          | -9223372036854775807 (-2^63+1) or less*   |
| LLONG_MAX  | Maximum value for an object of type *long long int*          | 9223372036854775807 (2^63-1) or less*     |
| ULLONG_MAX | Maximum value for an object of type *unsigned long long int* | 18446744073709551615 (2^64-1) or greater* |
`*` The actual value depends on the particular system and library implementation, but shall reflect the limits of these types in the target platform.

```cpp title:PracticalUsage
#include <climits>
#include <iostream>

int main() {
    std::cout << "The maximum value for int is: " << INT_MAX << std::endl;
    return 0;
}
```