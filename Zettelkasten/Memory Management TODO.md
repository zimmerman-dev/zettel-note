#### 📝 Note: Memory Management TODO 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚3:38 pm  📆 Sun Aug 17
 🔗 **Related Concepts**: #note #cpp
___
### **Phase 1 – Strip Down to C Basics**
The idea here is to re-learn familiar constructs without C++ sugar, while asking _“where is this in memory?”_ every step.
**Topics:**
- `#include <stdio.h>` instead of `<iostream>` — no `cout`, use `printf`.
- No `new`/`delete`, no STL — just arrays, pointers, `malloc`/`free`.
- `struct` has no methods, no constructors.
- Function prototypes go _above_ `main` or in headers.
#### **Mini-Exercise:**
```c
#include <stdio.h>

void printValue(int val) {
    printf("val = %d, address = %p\n", val, (void*)&val);
}

int main(void) {
    int x = 42;
    printf("x = %d, address = %p\n", x, (void*)&x);
    printValue(x);
}
```
> **Goal:** Notice `val` and `x` have different addresses — same value, different stack frames.
---
### **Phase 2 – Stack Frames**
Learn that local variables live on the stack and vanish after the function returns.
#### Mini-Exercise:
```c
#include <stdio.h>

void makeLocal(void) {
    int local = 123;
    printf("local = %d, address = %p\n", local, (void*)&local);
}

int main(void) {
    makeLocal();
    makeLocal();
}
```
> **Goal:** Notice addresses are close together or sometimes identical — memory is reused.
---
### **Phase 3 – Heap Allocations**
Get comfortable with `malloc`, `calloc`, `free`.
#### Mini-Exercise:
```c
#include <stdio.h>
#include <stdlib.h>

int main(void) {
    int *p = malloc(sizeof(int));
    *p = 99;
    printf("p points to %p with value %d\n", (void*)p, *p);
    free(p);
}
```
> **Goal:** See that heap addresses are far away from stack addresses, and memory must be freed manually.
---
### **Phase 4 – Pointer Arithmetic**
Understand that pointer math is scaled by `sizeof(type)`.
#### Mini-Exercise:
```c
#include <stdio.h>

int main(void) {
    int arr[3] = {10, 20, 30};
    int *p = arr;
    printf("%p -> %d\n", (void*)p, *p);
    p++;
    printf("%p -> %d\n", (void*)p, *p);
}
```
> **Goal:** See how addresses move by 4 bytes on a 32-bit int.
---
### **Phase 5 – Passing by Pointer**
Simulate “pass-by-reference” using pointers.
#### Mini-Exercise:
```c
#include <stdio.h>

void setToTen(int *ptr) {
    *ptr = 10;
}

int main(void) {
    int x = 5;
    setToTen(&x);
    printf("%d\n", x);
}
```
> **Goal:** Understand that now the callee and caller are working with the same stack location.
---
### **Phase 6 – Visualize**
After each exercise:
- **Draw the stack and heap** on paper.
- Mark addresses and variable lifetimes.
- Note when memory is created and destroyed.
---
### Memory Visualization Diagram
```
 ⬇️ High Memory Addresses ⬇️
+-----------------------------+
|     Command-line args       |  <-- Optional
|     Environment vars        |  
+-----------------------------+
|          STACK               |  <-- Grows DOWN toward heap
|  (local vars, function       |
|   parameters, return addrs)  |
+-----------------------------+
|   Unused gap / free space    |
|  (stack grows down, heap up) |
+-----------------------------+
|           HEAP               |  <-- Grows UP toward stack
| (malloc, calloc, realloc)    |
+-----------------------------+
|   Uninitialized data (BSS)   |  <-- Global/static vars set to 0
+-----------------------------+
|   Initialized data (DATA)    |  <-- Global/static vars with values
+-----------------------------+
|           TEXT               |  <-- Program code (instructions)
+-----------------------------+
  ⬆️ Low Memory Addresses ⬆️
```
#### Diagram Legend
- **TEXT segment:** your compiled instructions live here; read-only.
- **DATA segment:** global/static variables with initial values.
- **BSS segment:** global/static variables without initial values.
- **HEAP:** grows upward when you `malloc` memory.
- **STACK:** grows downward with each function call, adding a _stack frame_ for local vars and return info.
- There’s usually unused space between stack and heap — if they meet, you’ve run out of memory.