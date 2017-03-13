---
layout: default
permalink: /RE101/section1.2/
title: Fundamentals
---
[Go Back to Reverse Engineering Malware 101](https://securedorg.github.io/RE101/)

# Section 1.2: Fundamentals #

## Anatomy of a Windows PE C program ##

Typical windows programs are in the Portable Executable (PE) Format. It’s portable because it contains information, resources, and references to dynamic-linked libraries (DLL) that allows windows to load and execute the machine code. 

![alt text](https://securedorg.github.io/images/Cprogram.gif "C Program")

---

## Windows Architecture ##

In this workshop we will be focusing on user-mode applications.

### User-mode vs. Kernel Mode [1] ###

- In user-mode, an application starts a user-mode process which comes with its own private virtual address space and handle table

- In kernel mode, applications share virtual address space.

[1](https://msdn.microsoft.com/en-us/windows/hardware/drivers/gettingstarted/user-mode-and-kernel-mode?f=255&MSPPError=-2147217396)

This diagram shows the relationship of application components for user-mode and kernel-mode.
![alt text](https://securedorg.github.io/images/WindowsArch.png "Windows Architecture")

--- 

## PE Header ##

The PE header provides the information to operating system on how to map the file into memory.
The executable code has designated regions that require a different memory protection (RWX)
- Read
- Write
- Execute

This diagram shows how this header is broken up.
![alt text](https://securedorg.github.io/images/PE32.png "PE 32 Header")

Here is a hexcode dump of a PE header we will be working with.
![alt text](https://securedorg.github.io/images/PEHeader.gif "PE 32 Header Animated")

---

## Memory Layout ##

This diagram illustrates how the PE is placed into memory.
![alt text](https://securedorg.github.io/images/Memory.png "PE Memory Layout")

--- 

## The Stack ##

[Environment Setup <- Back](https://securedorg.github.io/RE101/section1) | [Next -> x86 Assembly](https://securedorg.github.io/RE101/section1.3)
