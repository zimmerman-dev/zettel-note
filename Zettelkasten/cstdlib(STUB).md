#### 📝 Note: cstdlib 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚7:32 pm  📆 Wed Aug 6
 🔗 **Related Concepts**: #note #cpp [[Functions - Built-in]] , [[Standard Library(STUB)]] , [[Data Types]] , [[Type Casting]] , [[random(STUB)]]

___

### 🎲 `<cstdlib>` — String Conversion Functions

These functions convert `char*` → numeric types (and vice versa in some cases):


| Function               | Purpose                          |
| ---------------------- | -------------------------------- |
| `atoi(const char*)`    | Convert string to `int`          |
| `atof(const char*)`    | Convert string to `double`       |
| `strtol()`             | Safer, flexible string → `long`  |
| `strtoul()`            | Unsigned version                 |
| `strod()` / `strtof()` | Convert to `double` / `float`    |
| `getenv(const char*)`  | Get environment variable by name |
| `system(const char*)`  | Run shell command from string    |
##### 🚫 `atoi()` and friends do no error checking—prefer `strtol()` where possible.