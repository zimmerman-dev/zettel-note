#### 📝 Note: Data Types 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:19 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #cpp #note [[Variables and Constants]] , [[Sizeof]]
___
#### Primitive Data Types:
These are the fundamental data types implemented directly by the C++ language. These include:

>[!info] Character Types
>- Used to represent single characters, e.g., 'A', 'X', '@', '%', etc.
>- Wider types are used to represent wide character sets.

| Type Name | Size/Precision                                     |
| --------- | -------------------------------------------------- |
| char      | Exactly one byte. At least 8 bits.                 |
| char16_t  | At least 16 bits.                                  |
| char32_t  | At least 32 bits.                                  |
| wchar_t   | Can represent the largest available character set. |
>[!info] Integer Types
> - Used to represent whole numbers.
> - Has both signed and unsigned versions.

| Type Name (signed)           | Size/Precision    |
| ---------------------------- | ----------------- |
| *signed* __short__ *int*     | At least 16 bits. |
| *signed* __int__             | At least 16 bits. |
| *signed* __long__ *int*      | At least 32 bits. |
| *signed* __long long__ *int* | At least 64 bits. |

| Type Name (unsigned)         | Size/Precision    |
| ---------------------------- | ----------------- |
| __unsigned short__ *int*     | At least 16 bits. |
| __unsigned__ *int*           | At least 16 bits. |
| __unsigned long__ *int*      | At least 32 bits. |
| __unsigned long long__ *int* | At least 64 bits. |


>[!info] Floating-point Types
>- Used to represent non-integer numbers.
>- Represented by mantissa and exponent (scientific notation).
>- Precision and size are compiler dependent

| Type Name   | Size/Typical Precision                  | Typical Range                   |
| ----------- | --------------------------------------- | ------------------------------- |
| float       | /7 decimal digits                       | 1.2 x 10^-38 to 3.4 x 10^38     |
| double      | No less than float / 15 decimal digits  | 2.2 x 10^-308 to 1.8 x 10^308   |
| long double | No less than double / 19 decimal digits | 3.3 x 10^-4932 to 1.2 x 10^4932 |

>[!info] Boolean Types
>- Used to represent true and false values.
>- Zero is false.
>- Non-zero is true.

| Type Name | Size/Precision                               |
| --------- | -------------------------------------------- |
| bool      | Usually 8 bits, true or false (C++ Keywords) |


>[!question] Remember:
>Unlike higher level programming languages, strings are not built in data types. String manipulation requires the use of the [[String|<string>]] library.
#### Type Sizes
The size of the data types are expressed in bits, which means that the more bits a data type can hold means the more values that can be represented. Thus the more bits also means the more storage required. Memory management is an important feature to understand in C++.

| Size (in bits) | Representable Values       |      |
| -------------- | -------------------------- | ---- |
| 8              | 256                        | 2^8  |
| 16             | 65,536                     | 2^16 |
| 32             | 4,294,967,296              | 2^32 |
| 64             | 18,446,744,073,709,551,615 | 2^64 |
[[Sizeof|see more on the sizeof operator for more details]]
