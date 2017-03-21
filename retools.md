---
layout: default
permalink: /RE101/section3/
title: RE Tools
---
[Go Back to Reverse Engineering Malware 101](https://securedorg.github.io/RE101/)

# Section 3: Reverse Engineering (RE) Tools #


## Disassemblers

* [Ida](https://www.hex-rays.com/products/ida/)
  * Free (Used in this worksop)
  * Pro (Most Popular)
* [Radare](https://www.radare.org)
* [Capstone](http://www.capstone-engine.org/)

---

### Disassembler: IdaFree

* **Visual Modes**
  * **Graph Mode** - control flow diagram
  * **Text Mode** - default view of disassembled code
* **Command Cheatsheet**
  * Please refer to this [Ida cheatsheet](https://securedorg.github.io/idacheatsheet.html)
* **Common Commands**
| Action | Command |
| --- | --- |
| Jump to xref to operand | X |
| Jump to address | G |
| Enter comment	| Shift+; |

## Debuggers

* [x64dbg](http://x64dbg.com/) (Used in this worksop)
* [Immunity](https://www.immunityinc.com/products/debugger/)
* [OllyDbg](http://www.ollydbg.de/)  (Most Popular)
* [WinDbg](https://developer.microsoft.com/en-us/windows/hardware/windows-driver-kit)

---

### Debugger: x64dbg

![alt text](https://securedorg.github.io/images/x64dbg.gif "x64dbg Layout")

**Common Commands**

| Action | Command |
| --- | --- |
| Enter comment	| Shift+; |
| BreakPoint	| F2 |
| Step into	| F7 |
| Step over	| F8 |
| Run	| F9 |
| Edit Instruction | Enter |

### Keyboard Layout for IdaFree and x64dbg

![alt text](https://securedorg.github.io/images/keyboarddbg.gif "Keyboad Layout")

---

## Decompilers

* [Snowman](https://derevenets.com/) (Integrated with x64dbg)
* [dotPeek](https://www.jetbrains.com/decompiler/) .NET decompiler

---

## Information Gathering

* [CFF Explorer](http://www.ntcore.com/exsuite.php) - PE header parser (Used in this worksop)
* [Sysinternals Suite](https://technet.microsoft.com/en-us/sysinternals/bb842062.aspx) (Used in this worksop)
  * procmon
  * procexplorer
* [InetSim: Internet Services Simulation Suite](http://www.inetsim.org/downloads.html) (Used in this worksop)
* [Yara: pattern matching rule engine](https://virustotal.github.io/yara/)
* [Wireshark](https://www.wireshark.org/download.html) - network sniffing (Used in this worksop)
* [API Monitor](http://www.rohitab.com/downloads)

---

## Information Gathering: CFF Explorer

* Parses the PE headers
* Explores Resources
* Unpacks UPX

![alt text](https://securedorg.github.io/images/CFFexplorer.gif "CFF Explorer")

## Information Gathering: Sysinternals Suite

* advanced system utilities
* **Procmon** - Monitor processes running on the system

![alt text](https://securedorg.github.io/images/procmon.png "Procmon")

---
  
## Support

* [HxD Hex Editor](https://mh-nexus.de/en/hxd/) (Used in this worksop)
* [Python](https://www.python.org/downloads/) - used for automating tasks


[Section 2.1 <- Back](https://securedorg.github.io/RE101/section2.1) | [Next -> Section 4](https://securedorg.github.io/RE101/section4)
