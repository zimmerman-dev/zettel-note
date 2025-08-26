 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚4:58 pm  📆 Mon Aug 25
 🔗 **Related Concepts**: #note #cpp
___
## 📝 Note: Introduction to Programming
While computers are incredibly fast and getting faster all the time, they also have some significant constraints: they only natively understand a limited set of instructions, and must be told exactly what to do.

A **computer program** is a sequence of instructions that tells a computer what to do, and in what order. These instructions are usually written in a **programming language** — a structured system of code. A **compiler** acts as a kind of decoder, translating that code into an executable form the computer can understand and run.

When the computer does the thing we ask, it's called **executing** the program, and it won't execute unless being told to do so. These programs run on your computers **hardware**, which consists of these typical pieces:

1. **CPU**: The Central Processing Unit, often called the "brain" of a computer, which actually executes the program.
2. **Memory**: This is where the programs are loaded prior to execution.
3. **Interactive Devices**: Keyboard, Mouse, Monitor, etc., these are things that make it possible to interact with the computer.
4. **Storage**: HDD, SSD, Flash Memory, etc., these parts retain data, even when the computer is not running.

In contrast, the term **software** broadly refers to programs on a system that are designed to be executed on hardware. The term **platform** refers to a compatible set of hardware and software (OS, Browser, etc...) that provides an environment, or layers of environments for software to run. If a program can be easily transferred to one platform to an another is said to be **portable**, and when a piece of software that only runs on a specific platform is made to be portable, this would be referred to as **porting** the software to other platforms.

Before when we talked about programming languages, we touched on how the programming language is like coded language and the compiler is our "Rosetta Stone", **Assembly** is what our coded message looks like on the other end. It's still *words* in its own way--what's called an instruction set for the CPU, though not yet usable by the computer to execute the program.

With that in mind, we can peel back the layers on the compiler. Conceptually, a compiler performs the roles of both an interpreter (understanding source code) and an assembler (producing machine instructions). In practice, modern compilers usually go straight from source to machine code, sometimes emitting assembly as an intermediate step.

So to recap our layers of abstraction:
```text
   Source Code (C++)
    ↓ Compiler
  Assembly Language
   ↓ Assembler
Machine Code (Opcodes in binary)
   ↓ CPU executes
Physical actions in hardware
   ↓
Observable behavior (your program running)
```
---
### 📌 Key Definitions
- **Computer Program**:  A sequence of instructions that tells a computer what to do, and in what order.
- **Programming Language**: A human readable language designed to facilitate the writing of instructions for computers.
-  **CPU**: The Central Processing Unit, often called the "brain" of a computer, which actually executes the program.
- **Memory**: This is where the programs are loaded prior to execution.
- **Interactive Devices**: Keyboard, Mouse, Monitor, etc., these are things that make it possible to interact with the computer.
- **Storage**: HDD, SDD, Flash Memory, etc., these parts retain data, even when the computer is not running.
- **Software**: Refers to programs on system that are designed to be executed on hardware.
-  **Assembly Language**: (often called **assembly** for short) is a programming language that essentially functions as a more human-readable machine language.
- **Machine Language**: A computer's native, lowest-level programming language, consisting of binary numbers (1s and 0s) that the CPU directly understands and executes.
- **Compiler**: a program that converts instructions into a machine-code or lower-level form so that they can be read and executed by a computer.
- **Assembler**: A program that converts human-readable assembly into machine code.
---
### 🧠 Flashcards

