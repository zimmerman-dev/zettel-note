#### 📝 Note: Tuple 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:27 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #cpp #note [[Standard Library Reference]] , [[C++ Syntax Reference]] , [[Templates and Generics]] , [[Functions]]
___
## 📦 So, what’s a tuple?

A **tuple** is a way to **bundle multiple values together** into a single unit, even if those values are different types.

Think of it like a tiny, unnamed package:

```cpp title:Syntax
std::tuple<T1, T2, T3> tuple_name;
```

- `std::tuple` is a **template class**.
- inside the angle brackets `< >`, you list the **types** of each element.
	- Yes types... As in multiple different types.

You can mix and match _any_ types:

- Primitives (`int`, `char`, `float`)
- STL containers (`std::vector`, `std::map`)
- Pointers (`int*`, `char*`)
- User-defined types (`MyStruct`, `Enemy`, etc.)

The only constraint is that **you must specify each type in order**, and you can only access elements by position—not by name.

---
## 🧱 Declaring a Tuple

```cpp title:Example.1
std::tuple<int, std::string, bool> person;
```

The tuple above is holding three distinct types:
1. an `int` 
2. a `std::string`
3. a `bool`

### 🏗 2. Initializing a Tuple

```cpp title:Example.2
std::tuple<int, std::string, bool> person = std::make_tuple(7, "Kepler", true);
```

The tuple above is holding three distinct types, initialized with values:
1. an `int` (7)
2. a `std::string` ("Kepler")
3. a `bool` (`true`)

question about the term "inferred types"

---
### 📦 3. Accessing Tuple Elements

Syntax:   `std::get<N>(tuple_name);`

- Like an array or vector, tuples are zero-indexed, but you can't access them exactly like an array or vector due to different types.
- The index must be known **at compile time** (a literal).

```cpp title:Example.3
std::tuple<int, std::string, bool> person = std::make_tuple(7, "Kepler", true);

int age {std::get<0>(person)};
std::string name {std::get<1>(person)};
bool alive {std::get<2>(person)};

std::cout << "The person's age is: " << age << std::endl;
std::cout << "The person's name is: " << name << std::endl;
std::cout << "The person is alive? ";

if (alive) {
	std::cout << "Yes!" << std::endl;
} else {
std::cout << "No..." << std::endl;
}
return 0;
```


### 🪄 4. Structured Bindings (C++17+)

Syntax:   `auto [id, name, alive] = person;`

- This unpacks the tuple into name variables
- It's cleaner and more readable, and is generally considered best practices for C++ when available.


>[!note] Inferred Types
> When you use `std::make_tuple(...)`, the compiler **automatically deduces** the types of the values you pass in.
> 

>[!note] So:
`auto person = std::make_tuple(7, "Kepler", true);`

>[!note] …is equivalent to writing:
`std::tuple<int, const char*, bool> person = std::make_tuple(7, "Kepler", true);`

>[!note] Although:
> `"Kepler"` is a C-string literal, it often gets stored as `const char*` unless explicitly converted to `std::string`.)

---
#### 🎯 Why Tuples Are Useful

Tuples are like **ad hoc structs** for when:
- You don’t want to define a full struct or class
- You just need to pass or return multiple values quickly
- You don’t need named fields—just a temporary bundle

#### 🤔 When _not_ to use a tuple

- If the values need **names**, not just positions → use a `struct`
- If there are **too many elements** → it becomes unreadable
- If you want **clarity over brevity** → tuples can get cryptic fast