 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚7:07 pm  📆 Tue Sep 30
 🔗 **Related Concepts**: #note #cpp
___
## 📝 Note: Demangler Codes for GCC
These are the one-letter codes you’ll see when calling `typeid(...).name()` without demangling.

| Code | Type                  |
|------|-----------------------|
| v    | void                  |
| w    | wchar_t               |
| b    | bool                  |
| c    | char                  |
| a    | signed char           |
| h    | unsigned char         |
| s    | short                 |
| t    | unsigned short        |
| i    | int                   |
| j    | unsigned int          |
| l    | long                  |
| m    | unsigned long         |
| x    | long long             |
| y    | unsigned long long    |
| f    | float                 |
| d    | double                |
| e    | long double           |

⚠️ For user-defined types and standard library types e.g., `std::string`,  you’ll get a mangled name like `St6string` or starting with `N...`.  Use a demangler e.g. `abi::__cxa_demangle` if you need to decode those.