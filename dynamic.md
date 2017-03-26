---
layout: default
permalink: /RE101/section6/
title: Dynamic Analysis
---
[Go Back to Reverse Engineering Malware 101](https://securedorg.github.io/RE101/)

# Section 6: Dynamic Analysis #

![alt text](https://securedorg.github.io/images/hackerman.gif "hackerman")

## LAB 3
Dynamic analysis is a deeper analysis of the program to understand hidden functionality not understood statically. The static analysis will serve as a guide for stepping through the program in a debugger.

Open the unpacked malware into the **x64dbg** debugger and **IDAfree**.

### Rebasing the disassembler

Typically programs start at **004010000** but your debugger might start the program at a different address. You will need to rebase the program's address in the disassembler. In x64dbg, scroll up to find the very first address, this is the address that you will need to rebase. Edit->Segements->Rebase Program.
![alt text](https://securedorg.github.io/images/dyn2.png "Victim and Sniffer")

### Finding the starting point

You will need to sync the debugger and disassembler addresses so you can follow along in both. Let's start with the function offset **xxxx1530**.
* In IDA, open the functions tab and look for function xxxx1530. Where xxxx should match your rebase address ( If rebase is 01901000, then 01901530 ).
* In x64dbg, CTRL+G to jump to a specific address xxxx1530.

![alt text](https://securedorg.github.io/images/dyn3.png "IDAmain")
![alt text](https://securedorg.github.io/images/dyn4.png "x64dbg Jump")

[Section 5 <- Back](https://securedorg.github.io/RE101/section5)