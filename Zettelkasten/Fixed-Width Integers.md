 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚8:36 pm  📆 Sun Sep 7
 🔗 **Related Concepts**: #note #cpp [[Signed Integers]] , [[Unsigned Integers]] , [[Fundamental Data Types]] , [[Sizeof Operator]] , [[climits]] 
___
## 📝 Note: Fixed-Width Integers
So, we know C++ only guarantees that integer variables **will have a minimum size** -- but they could be larger, depending on the target system. The common example is that an `int` has a minimum size of 16-bits, but it's typically 32-bits on modern architectures.  
--- start-multi-column: ID_onqa

```column-settings
Number of Columns: 2
Largest Column: Left
Column Spacing: 3px
Border: off
```
#### Caveat
If you assume an `int` is always 32-bits (because that’s common on modern systems), your program may misbehave on an architecture where `int` is actually 16-bits. In that case, storing a 32-bit-sized value in a 16-bit variable can cause overflow and undefined behavior.

On the other hand, if you always assume `int` is only 16-bits to stay portable, then on 32-bit systems you’re unnecessarily limiting the range of values you can safely store, even though the extra capacity is available.

--- column-break ---

#### Key insight
In most cases, we only instantiate a small number of `int` variables at a time, and these are typically destroyed at the end of the function in which they are created. With that in mind, 2 bytes of memory is drop in the bucket (the limited range is a bigger concern). However, in cases where our program allocates millions of `int` variables, wasting 2 bytes of memory per variable can have a significant impact on the programs performance.

--- end-multi-column
#### Why isn't the size of the `int` fixed?
Historically, this goes back to traditions in **C programming**, when computers were slow and performance was the top priority. C was designed to intentionally leave the size of `int` open so compiler implementers could pick a size that performed best on the target CPU architecture.

In modern times, this flexibility creates a portability challenge: the size of `int` can vary between systems, which makes it harder to write code that behaves consistently across platforms. This is exactly why C++ introduced fixed-width integer types (like `int32_t` and `uint64_t`) — to give developers precise control when consistency matters more than raw speed.
___
### 🔹`#include <cstdint>`
C++11 set out to address the above issues by providing an alternate set of integer types that are guaranteed to be the same size on any architecture. It may seem obvious, but **fixed-width integers** are integers with a fixed size. The fixed-width integers are defined (`<cstdint>` header) as follows:

|       Name       | Fixed size |        Fixed Range        |
| :--------------: | :--------: | :-----------------------: |
| `std::int8_t` ⭐  |   1 byte   |        -128 to 127        |
| `std::uint8_t` ⭐ |   1 byte   |         0 to 255          |
|  `std::int16_t`  |  2 bytes   |      -32768 to 32767      |
| `std::uint16_t`  |  2 bytes   |        0 to 65535         |
|  `std::int32_t`  |  4 bytes   | -2147483648 to 2147483647 |
| `std::uint32_t`  |  4 bytes   |      0 to 4294967295      |
|  `std::int64_t`  |  8 bytes   |    -(2^63) to (2^63)-1    |
| `std::uint64_t`  |  8 bytes   |       0 to (2^64)-1       |
`std::int8_t` and `std::uint8_t` are starred because they are both treated like 8-bit chars, singed and unsigned respectively. So if you store a numeric value in an object with those types, the compiler may interpret those values as ascii. This leads me to the next important detail about **fixed-width integers**.
### 🔹 Key Insight
`cstdint` doesn't actually create new integer types, but creates 'typedefs', or aliases, for existing integral types. For example: on a **32 bit system**, `std::int32_t` is an alias for `int`. If that system represents `int` as 16 bit, `std::int32_t` would be an alias for a `long`.

With that in mind, lets re-address the statement above:
> _`std::int8_t` and `std::uint8_t` are starred because they are both treated like 8-bit chars, singed and unsigned respectively._

With this:
> `std::int8_t` and its unsigned counterpart `std::uint8_t` are both just **aliases** for chars, signed and unsigned respectively.

See: [[Char]] and [[Type Conversion - Overview]] for more info on this.
___
### 🔹 Quibbles with Fixed-width `int`
There are two main quibbles with the `<cstdint>` header.

1. While it is unlikely, not all systems have defined fixed-width integers.
2. Fixed-width integers may be slower, less performant on some architectures.
#### Fast and Least
To help address these minor objections, C++ also defines two alternative sets of integers that are guaranteed to exist:
##### Fast: `std::int_fast#_t` and `std::uint_fast#_t`
These are defined to provide the **fastest** signed/unsigned integer types with at least # bits (# = 8, 16, 32, 64). In this context, _fastest_ means the integral type that can be most quickly processed by the system.
##### Least: `std::int_least#_t` and `std::uint_least#_t`
These are defined to provide the **smallest** integer type with a width of at least # bits (# = 8, 16, 32, 64). For example: `std::int_least32_t` will give you the smallest integer type on your system that is at least 32 bits.
##### Best Practices
Avoid using fast and least. It seems like it can be useful, though it can cause issues with portability.
___
### 🔹 `std::size_t`
To simplify, `size_t` is just an unsigned integer type of your compiler’s choosing, chosen based on the system's architecture. It is useful because it guarantees the ability to hold the size (in bytes) of any object, and it abstracts away differences between systems.

To compare: if `std::int32_t` is a **typedef** (alias) for an integer, `std::size_t` is an alias for an implementation-defined **unsigned** integral type.
#### General "Rules" for `size_t`
1. Even though `sizeof` (which doesn't require a header) will return a value whose type is `std::size_t`, you still need to `#include <cstddef>` or a related header to use `std::size_t` by name.

2. `std::size_t` is guaranteed to be at least 16 bits, but on most systems, it's equivalent to the address-width of the application (e.g., 32-bit or 64-bit).

3. `std::size_t` is always unsigned — sizes and memory offsets cannot be negative.

4. `std::size_t` defines the **maximum theoretical object size**, though real-world limits (compiler, OS, RAM) are usually lower.


#### Usage Rule of Thumb
Use `std::size_t` when counting memory, sizes, or array indexes — anywhere negative numbers don't make sense and unsigned arithmetic is safer.
#### Practical Limits
While `size_t` defines the theoretical maximum size an object can have (based on its max value), many systems restrict the largest _creatable_ object:

- Compilers may cap allocation size to **half** of `size_t`'s max.

- Your system may not have enough **contiguous free memory** to fulfill large allocations.

- OS, heap fragmentation, or virtual memory limits may reduce usable space.

So in practice, object size limits are almost always **less than `size_t`'s max**.
___
### 📌 Key Definitions
- **`std::intN_t` / `std::uintN_t`**  
    Fixed-width integer aliases that guarantee exactly N bits of storage (`N = 8, 16, 32, 64`). Provided in `<cstdint>`.
    
- **`typedef` / alias**  
    A way to give an existing type a new name. All fixed-width types are typedefs, not new fundamental types.
    
- **`std::size_t`**  
    An unsigned integer type large enough to represent the size (in bytes) of any object in memory. Returned by `sizeof` and used for indexing and allocation.
    
- **Theoretical object size limit**  
    The largest value `std::size_t` can hold (e.g., 2³²−1 on 32-bit systems), beyond which no single object can be represented.
    
- **Practical object size limit**  
    A system-dependent, usually smaller limit based on available memory, heap fragmentation, compiler caps, or OS constraints.
    
- **`int_fastN_t` / `int_leastN_t`**  
    Alternative fixed-width types:
    
    - `fast`: fastest available type ≥ N bits
        
    - `least`: smallest available type ≥ N bits  
        Not commonly used in modern code.
---
### 🧠 Flashcards

What is `std::int32_t`?  
?|?  
A typedef (alias) for a signed 32-bit integer type, guaranteed to be exactly 32 bits wide.

---

Is `std::int8_t` a new type?  
?|?  
No — it’s an alias, typically for `signed char`.

---

What header defines fixed-width integer types like `int32_t`?  
?|?  
`<cstdint>`

---

What are `int_fast32_t` and `int_least32_t`?  
?|?  
Alternative fixed-width integer aliases:

- `fast` = fastest type ≥ N bits
- `least` = smallest type ≥ N bits

---

What is `std::size_t`?  
?|?  
An unsigned integer type defined by the compiler, guaranteed to hold the size (in bytes) of any object.

---

Why is `size_t` unsigned?  
?|?  
Because sizes and indexes are never negative.

---

What does it mean when we say "`size_t` is implementation-defined"?  
?|?  
The exact type (`unsigned int`, `unsigned long`, etc.) is chosen by the compiler and may vary between systems.

---

What’s the difference between the theoretical and practical object size limits?  
?|?  
The **theoretical limit** is the max value `size_t` can represent.  
The **practical limit** is usually smaller, due to compiler/OS/memory constraints.

---

What is returned by the `sizeof` operator?  
?|?  
A value of type `std::size_t`, representing the size (in bytes) of an object or type.

---

When should you use `size_t`?  
?|?  
When counting memory, sizes, or array indexes — anywhere negative numbers don’t make sense and unsigned safety matters.

#flashcards 