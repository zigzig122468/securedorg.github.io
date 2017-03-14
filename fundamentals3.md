---
layout: default
permalink: /RE101/section1.3/
title: Fundamentals
---
[Go Back to Reverse Engineering Malware 101](https://securedorg.github.io/RE101/)

# Section 1.3: Fundamentals #

## x86 Assembly ##

The C programming is a high level language interpreted by the compiler that converts code into machine instructions called assembly language. By using a disassembler tool we can get the assembly language of a compiled C program.

### Opcodes and Instructions ###

Each Instruction represents opcodes (hex code) that tell the machine what to do next.

Three categories of instructions:
* data movement
* arithmetic/logic
* control-flow.

Common Instructions
* push, pop, call, leave, enter, ret
* mov
* lea
* add,sub
* jmp,jne,jnz,jnb
* or, and, xor
* shr,shl
* ror,rol

Use the search page below or open the [Search Instructions](https://securedorg.github.io/x86.html) page to search for functions discussed above

<iframe src="https://securedorg.github.io/x86.html" width="640" height="480" frameborder="0" style="display:block; margin: 0 auto;"></iframe>


### Registers ###

## A Function and Calling a Function ##

### Arguments ###

### Local Variables ###

### The Stack ###

[Anatomy of PE <- Back](https://securedorg.github.io/RE101/section1.2) | [Next -> Section 2](https://securedorg.github.io/RE101/section2)
