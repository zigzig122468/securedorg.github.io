---
layout: default
permalink: /RE101/section5/
title: Static Analysis
---
[Go Back to Reverse Engineering Malware 101](https://securedorg.github.io/RE101/)

# Section 5: Static Analysis #

Static analysis is like reading a map for directions on where to go. As you follow through this map you capture notes on what things might look interesting when you actually begin your journey.

This section will teach you how to jump into code in static disassembly then rename and comment on interesting assembly routines that we will debug in **Section 6**.


## LAB 2

### Possible Packer?
Notice in CFF explorer that there is UPX in the header.

![alt text](https://securedorg.github.io/images/triage2.png "UPX")

When you open the executable in IDA, you will notice large section of non-disassembled code.

![alt text](https://securedorg.github.io/images/triage4.png "IDA UPX")

Because UPX is a common packer, the unpacker is already built in to CFF Explorer. Unpack and save the file with a name that identifies it as unpacked.

![alt text](https://securedorg.github.io/images/triage5.png "Unpacking UPX")

---

### Reopen the executable in IDA.

The next step is getting a sense as to what the program is doing.
So far we can assume:
* This exe is connecting to the internet somehow
* This exe is using a string encryption function
* This exe might be spawning a shell

Most windows programs start at address **004010000**.

---

### Jumping in!

Navigate to the **Strings** window.

Here is an interesting string that we should start with:

![alt text](https://securedorg.github.io/images/static1.png "Strings window")

This string is a typical registry key path to allow programs to autorun/startup on reboot. This is considered a [persistence](https://securedorg.github.io/RE101/section2.1/#persistence) mechanism. Double Click the string.

Using the **X** key we can jump to the reference of that string in the assembly code.

![alt text](https://securedorg.github.io/images/static2.gif "Strings window")

This function is offset **00401340**. Notice in that function is setting a registry key using Window API [RegOpenKeyEx](https://msdn.microsoft.com/en-us/library/windows/desktop/ms724897%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396).

We should rename this function **SetRegkey**.

---

Jump up to the calling function using **X** on **SetRegkey**. Scroll up until you see some interesting API.

Notice it's calling [InternetOpen](https://msdn.microsoft.com/en-us/library/windows/desktop/aa385096.aspx) which opens a HTTP session.

This function call has the following arguments:

**C++**

```c++
HINTERNET InternetOpen(
  _In_ LPCTSTR lpszAgent,      // Arg 1 = URL
  _In_ DWORD   dwAccessType,   // Arg 2
  _In_ LPCTSTR lpszProxyName,  // Arg 3
  _In_ LPCTSTR lpszProxyBypass,// Arg 4
  _In_ DWORD   dwFlags         // Arg 5
);
```

We need to figure out what register **esi** is because it contains the URL we are looking for.

**Assembly x86**

```assembly
push 0    ; Arg 5
push 0    ; Arg 4
push 0    ; Arg 3
push 1    ; Arg 2
push esi  ; Arg 1 URL
call ds: InternetOpenA
```

Right before the first **push 0** there is a **mov esi,eax** which means esi = eax.

When a function returns, the return value is stored in **eax**. So let's look into the function that is being called. It takes a string as the first argument (that is a wicked string), while the second argument might be the string length. Press Enter to jump to the function.

![alt text](https://securedorg.github.io/images/static3.png "Unknown Function")
 
Scroll down until you find **xor al, 5Ah**. Eventually you will be able to recognize when a string loop is being processed in assembly. In this case, it is **xor** a byte with **5Ah** which is **Z** in [ascii](http://www.asciitable.com/).
 
![alt text](https://securedorg.github.io/images/static4.png "Xor routine")

We can assume that this function is doing some kind of Xor encoding. So let's rename this function as XorDecode. We will need this information later when we debug in Section 6.

![alt text](https://securedorg.github.io/images/static5.png "Rename function")

Let's use the tool **XORSearch** to see if we can find some interesting xor decoded strings. Open the terminal **cmd.exe** from the start bar, and navigate to the XORSearch.exe

```XORSearch.exe <Path to Unknown.exe> "A string to test"```

![alt text](https://securedorg.github.io/images/static6.png "xor search")

**"Yo this is dope!"** How weird.

---

## Getting the bigger picture

Let's navigate to the start of the program using the **X** key. Use the spacebar to toggle between graph view and text view.

![alt text](https://securedorg.github.io/images/static7.gif "start function")

It's easy to trace back through the program disassembly, but let's look at some control flow assembly instructions. Remember **jmp, jne, jnz, jnb** are control flow functions.

**Jump Examples**

![alt text](https://securedorg.github.io/images/static9.gif "jz jump")

```assembly
jz loc_401962 ; jump too offset loc_401962 if the previous condition is zero
```

```assembly
jle short loc_401634 ; jump to relative offset 401634 if the previous condition is less than or equal to
```

Next scroll down through and find the order of API function calls in the program. You should make note of all the function offsets.

![alt text](https://securedorg.github.io/images/static8.gif "program scrolling")

Some of the more interesting API Calls from the image above. Look up what each function does, many are self explanatory.

* GetEnvironmentVariable
* CopyFile
* DeleteFile
* InternetOpen
* InternetConnect
* HttpOpenRequest
* HttpSendRequest
* MessageBox
* FindResource
* CryptStringToBinary
* CreateFile
* ShellExecute
* CreateProcess

Now you know how to navigate the disassembly forward and backwards to get to interesting routines. The next step is making a rough path to follow for deeper analysis in Section 6.

![alt text](https://securedorg.github.io/images/maping.jpg "handwritten")

[Section 4 <- Back](https://securedorg.github.io/RE101/section4) | [Next -> Section 6](https://securedorg.github.io/RE101/section6)
