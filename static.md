---
layout: default
permalink: /RE101/section5/
title: Static Analysis
---
[Go Back to Reverse Engineering Malware 101](https://securedorg.github.io/RE101/)

# Section 5: Static Analysis #

## LAB 1

### Possible Packer?
Notice in CFF explorer that there is UPX in the header.
![alt text](https://securedorg.github.io/images/triage2.png "UPX")

When you open the executable in IDA, you will notice large section of non-disassembled code.
![alt text](https://securedorg.github.io/images/triage4.png "IDA UPX")

Because UPX is a common packer, the unpacker is already built in to CFF Explorer. Unpack and save the file with a name that identifies it as unpacked.
![alt text](https://securedorg.github.io/images/triage5.png "Unpacking UPX")

### Reopen the executable in IDA.

The next step is getting a sense as to what the program is doing.
So far we can assume:
* This exe is connecting to the internet somehow
* This exe is using a string encryption function
* This exe might be spawning a shell

---

Navigate to the **String** window.

Here is an interesting string that we should start with:
![alt text](https://securedorg.github.io/images/static1.png "Strings window")

Using the **X** key we can jump to the reference of that string in the assembly code.
![alt text](https://securedorg.github.io/images/static2.gif "Strings window")

This function is offset **00401340**. Notice in that function is setting a registry key using Window API [RegOpenKeyEx](https://msdn.microsoft.com/en-us/library/windows/desktop/ms724897%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396).

We should rename this function **SetRegkey**.

---

 

[Section 4 <- Back](https://securedorg.github.io/RE101/section4) | [Next -> Section 6](https://securedorg.github.io/RE101/section6)
