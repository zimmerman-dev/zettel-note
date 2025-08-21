#### 📝 Note: Constants 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:08 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #note #cpp [[Data Types]], [[Variables and Constants]], [[Enums]]
___
## What is a Constant?
Like C++ variables, **constants** have names, occupy storage, are *usually* typed. 

>[!warning] 
>However; once declared, their value cannot be changed!

___
## Types of Constants in C++
#### Literal Constants
 The literal constant is the most obvious kind of constant, e.g.:
 
>[!Example] 
> `x = 12;`
> `y = 1.56;`
> `name = "frank";`
> `middle_initial = 'J';`

You can also declare a constant explicitly: 

>[!Example]
>`12; // an integer`
>`12U; // an unsigned integer`
>`12L; // a long integer`
>`12LL; // a long long integer`
##### Character Literal Constants
#### Declared Constants (`const` keyword)
Constant declared using the const keyword are the most common.

>[!Example]
>`const double pi{3.1415926};`
>`const int months_in_year{12};`
#### Defined Constants (`#define`)
The defined constants are used in old C++ code, and the way it works is as a preprocessor directive.

>[!Example] 
>`#define pi 3.1415926;`

>[!Warning]
>Don't use defined constants in Modern C++

#### Constant Expressions (`constexpr` keyword)
#### Enumerated Constants (`enum` keyword)