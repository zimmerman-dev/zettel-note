#### 📝 Note: cstring 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚1:01 am  📆 Wed Aug 6
 🔗 **Related Concepts**: #note #cpp [[C-Style Strings]] 
___
### 📚 `<cstring>` — String Manipulation Functions

These functions work directly on C-style strings (`char*` or `char[]`):


|         Function         |                  Purpose                  |
| :----------------------: | :---------------------------------------: |
|        `strlen()`        |   Get **length** of string (up to `\0`)   |
| `strcpy()` / `strncpy()` |        Copy one string to another         |
| `strcat()` / `strncat()` |       Append one string to another        |
| `strcmp()` / `strncmp()` |              Compare strings              |
| `strchr()` / `strrchar`  |         Find character in string          |
|        `strstr()`        |              Find substring               |
| `memcpy()` / `memmove()` | Raw memory copy (often used with `char*`) |
##### ⚠️ Watch for buffer overflows. These functions assume you know how much space you're working with.

