 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚9:38 am  📆 Mon Sep 1
 🔗 **Related Concepts**: #note #cpp
___
## 📝 Note: zimmerman-dev
```dataviewjs
// Show general vault stats
let s = await window.showStats();
dv.paragraph(s);

// Show last modified notes (default 10, excluding "Templates" folder)
let recent = await window.showLastModifiedNotes(10, "Templates");
dv.paragraph("### 🕒 Last Modified Notes:\n\n" + recent);
```
#### ✅ To-do: zimmerman-dev   
 ⌚10:58 pm  📆 Thu Sep 4
 🔗 **Related Concepts**: #todo
___
### 🔹 Week 3:  **09/09 – 09/15** — Fundamental Types & Literals  
📍 **Ch. 4 + Ch. 5** — _Data Types, Constants, Strings_  
- [x] **Block 1:** (4.1 → 4.5) Primitive types, signed/unsigned, object sizes  
- [ ] **Block 2:** (4.6 → 4.10) Fixed-width, floats, bool, if  
- [ ] **Block 3:** (4.11 → 5.4) Chars, `static_cast`, constants, numeral systems  
- [ ] **Weekend:** Chapter 4+5 quiz + type cheat sheet  


____
#### 🔥 Most important stuff for Chapter 4
 ♻️  
 ⌚8:46 pm  📆 Sun Sep 7
 🔗 **Related Concepts**: #note
___

- ✅ Type definitions (`int`, `short`, `long`, `float`, `char`, `bool`, etc.)
- ✅ Type sizes (platform-dependent vs fixed-width)
- ✅ Value ranges for common signed/unsigned types
- ✅ Behavior on **signed overflow** (undefined) vs **unsigned overflow** (wraparound)
- ✅ `sizeof` operator and how it applies to types/objects
- ✅ `size_t`: purpose, behavior, why it’s unsigned
- ✅ Fixed-width integers: `std::int8_t`, `std::uint32_t`, etc.
- ✅ Integer promotion rules (e.g. small types promote to `int`)
- ✅ Implicit vs explicit conversion (`static_cast`, narrowing)
- ✅ When to avoid unsigned (looping, underflow traps)
- ✅ Floating point format basics (scientific notation, `float` vs `double`)
- ✅ Boolean truthy/falsy behavior in C++
- ✅ ASCII basics for `char` and character literals