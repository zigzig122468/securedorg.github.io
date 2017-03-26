---
layout: default
permalink: /RE101/section4/
title: Triage Analysis
---
[Go Back to Reverse Engineering Malware 101](https://securedorg.github.io/RE101/)

# Section 4: Triage Analysis #

Depending on your workload, you want to spend the least amount of time trying to determine what the malware is doing and how to get rid of it. Many malware analysts use their own triage analysis, similar to that in the Emergency Room at the hospital.

You will want to quickly narrow down specific information and indicators before moving on to deeper static and dynamic analysis.

This checklist should get you started:

- File Context and Delivery
- File Information & Header Analysis
- Get Basic PE information
- Simple Search
- Collect Strings
- Check AV vendors
- Quick VM Detonation
- Capture network information

### File Context and Delivery

When you receive the malware binary, it's important to ask how the malware got there in the first place.

Questions to ask:
* Did it come from an email?
* Did it come from a browser download?
* Was it quarantined in an Anti-Virus?
* Is it an anomalous process running?

### File Information & Header Analysis

* Use a **file** command (sniffer VM) to determine the file type
* Verify the file header using a hex editor (HxD)

### Get Basic PE information

* Parse the PE header using the tool CFF Explorer
* Determine what resources, DLL imports, and libraries used
  * Example: If you see **Ws2_32.dll** it might be setting up a network connection because it's used for setting up sockets

### Simple Search

* Calculate the hash of the file an check the web to see if it's been seen already

### Collect Strings

* using the string command in linux or BinText tool, extract the strings to find any clues

### Check AV vendors

* Run the file against an Anti-Virus or VirusTotal to see if there are any detections

### Quick VM Detonation

* Use open source VM detonation services like hybrid-analysis.com or malwr.com to get the behavior quickly

### Capture network information

* Use the VM detonation service to capture any network connections or packet data.
* If you can't do this then we will need to dynamically debug the malware.

## Malware Analysis Report

You will want to capture this information throughout your investigation either through notes or report documents.

You can use the **Malware Analysis Report** template [HERE](https://securedorg.github.io/ReportForm.html)


## LAB 1

1. Run the Victim VM
2. Copy over the unknown file
3. Check the file header by opening the file in the hex editor **HxD**
* Notice the first 1 byte is **MZ** meaning it's a PE Binary
![alt text](https://securedorg.github.io/images/triage1.png "MZ Header")
4. Now right click the file and select **CFF explorer** to check the PE header
* Note the imports it's using
![alt text](https://securedorg.github.io/images/triage3.png "Imports")
5. Calculate the hash using **quickhash**, go to virustotal.com and search the hash
6. Open the file in **BinText** and record any interesting strings
7. Quick Detonation
The point of the quick detonation is to capture the filesystem, registry, and connection activity. The VMs are set up in such a way that the Victim VM's internet traffic is captured by the Sniffer VM.
![alt text](https://securedorg.github.io/images/triageVMs.gif "Victim and Sniffer")

On the **Sniffer VM** open the terminal and run `sudo wireshark` to get Wireshark sniffing the traffic from the Victim VM. Be sure InetSim is still running, see the fundamentals Section 1 on how to start up InetSim.

On the **Victim VM** open the SysInternals **procmon.exe** and **procexp.exe** so that we can monitor filesystem and process events.
![alt text](https://securedorg.github.io/images/triageVMs2.gif "Victim and Sniffer")

Go ahead and detonate the the malware.

On the **Sniffer VM** look for an HTTP request. Right click and Follow->TCP Stream. I will display the HTTP get request that was sent by the malware.
![alt text](https://securedorg.github.io/images/triageVMs3.gif "Victim and Sniffer")

[Section 3 <- Back](https://securedorg.github.io/RE101/section3) | [Next -> Section 5](https://securedorg.github.io/RE101/section5)
