---
layout: default
permalink: /RE101/section1.3/
title: Fundamentals
---
[Go Back to Reverse Engineering Malware 101](https://securedorg.github.io/RE101/)

# Section 1.3: Fundamentals #

## x86 Assembly Language ##

The C programming is a high level language interpreted by the compiler that converts code into machine instructions called assembly language. By using a disassembler tool we can get the assembly language of a compiled C program.

The Intel 8086 and 8088 were the first CPUs to have an instruction set that is now commonly referred to as **x86**. Intel Architecture 32-bit (IA-32) sometimes also called i386 is the 32-bit version of the x86 instruction set architecture.

The x86 architecture is **little-endian**, meaning that multi-byte values are written least significant byte first.

#### How we see it:
| A0 | A1 | A2 | A3 |

#### Stored as Little Endian
| A3 | A2 | A1 | A0 |

## Opcodes and Instructions ###

Each Instruction represents opcodes (hex code) that tell the machine what to do next.

Three categories of instructions:
* Data Movement
* Arithmetic / Logic
* Control-Flow

Common Instructions
* **mov, lea** (data movement)
* **add, sub** (arithmetic)
* **or, and, xor** (Logic)
* **shr, shl** (Logic)
* **ror, rol** (Logic)
* **jmp, jne, jnz, jnb** (Control Flow) 
* **push, pop, call, leave, enter, ret** (Control Flow)

Use the search page below or open the [Search Instructions](https://securedorg.github.io/x86.html) page to search for functions discussed above

<iframe src="https://securedorg.github.io/x86.html" width="640" height="480" frameborder="0" style="display:block; margin: 0 auto;"></iframe>

---

## Registers ###

The image below is what registers will look like in a debugger.
![alt text](https://securedorg.github.io/images/Registers.png "Registers")

#### General-Purpose Registers [[1]][1]


| Register | Description |
| --- | --- |
| **EAX** | Accumulator Register |
| **EBX** | Base Register |
| **ECX** | Counter Register |
| **EDX** | Data Register |
| **ESI** | Source Index |
| **EDI** | Destination Index |
| **EBP** | Base Pointer |
| **ESP** | Stack Pointer |

#### Segment Registers

| Register | Description |
| --- | --- |
| SS | Stack Segment, Pointer to the stack |
| CS | Code Segment, Pointer to the code |
| DS | Data Segment, Pointer to the data |
| ES | Extra Segment, Pointer to extra data |
| FS | F Segment, Pointer to more extra data |
| GS | G Segment, Pointer to still more extra data |

#### EFLAGS Register

| ID | Name | Description |
| --- | --- | --- |
| CF | Carry Flag | Set if the last arithmetic operation carried (addition) or borrowed (subtraction) a bit beyond the size of the register. This is then checked when the operation is followed with an add-with-carry or subtract-with-borrow to deal with values too large for just one register to contain |
| PF | Parity Flag | Set if the number of set bits in the least significant byte is a multiple of 2 |
| AF | Adjust Flag | Carry of Binary Code Decimal (BCD) numbers arithmetic operations |
| ZF | Zero Flag | Set if the result of an operation is Zero (0) |
| SF | Sign Flag | Set if the result of an operation is negative |
| TF | Trap Flag | Set if step by step debugging |
| IF | Interruption Flag | Set if interrupts are enabled |
| DF | Direction Flag | Stream direction. If set, string operations will decrement their pointer rather than incrementing it, reading memory backwards |
| OF | Overflow Flag | Set if signed arithmetic operations result in a value too large for the register to contain |
| IOPL | I/O Privilege Level field (2 bits) | I/O Privilege Level of the current process |
| NT | Nested Task flag | Controls chaining of interrupts. Set if the current process is linked to the next process |
| RF | Resume Flag | Response to debug exceptions |
| VM | Virtual-8086 Mode | Set if in 8086 compatibility mode |
| AC | Alignment Check | Set if alignment checking of memory references is done |
| VIF | Virtual Interrupt Flag | Virtual image of IF |
| VIP | Virtual Interrupt Pending flag | Set if an interrupt is pending |
| ID | Identification Flag | Support for CPUID instruction if can be set |

#### Instruction Pointer

The **EIP** register contains the address of the next instruction to be executed.

---

## A Function and Calling a Function ##

### Arguments ###

### Local Variables ###

### The Stack ###

[1]: https://en.wikibooks.org/wiki/X86_Assembly/X86_Architecture

[Anatomy of PE <- Back](https://securedorg.github.io/RE101/section1.2) | [Next -> Section 2](https://securedorg.github.io/RE101/section2)
