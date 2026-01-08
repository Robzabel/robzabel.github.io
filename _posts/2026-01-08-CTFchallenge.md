---
layout: post
title: CTF Reversing Engineering Challenge
---

![_config.yml]({{ site.baseurl }}/images/diaTitle.jpg)

## Cyberpsychosis Challenge from Hack The Box 

I have been really enjoying the reverse engineering challenges from HTB. I recently completed one that I found very interesting I will not post the name of the challenge or the flag to keep within HTB rules, but I wanted to do a write up as it involved a Linux root kit which is something I have not previously analysed.

### Challenge Scenario
Malicious actors have infiltrated our systems and we believe they've implanted a custom rootkit. Can you disarm the rootkit and find the hidden data?

#### File Command
I always start by running the file command on a binary to get as much infromation as possible about what I am looking at:
![_config.yml]({{ site.baseurl }}/images/filecommand.png)
diamorphine.ko: ELF 64-bit LSB relocatable, x86-64, version 1 (SYSV), BuildID[sha1]=e6a635e5bd8219ae93d2bc26574fff42dc4e1105, with debug_info, not stripped

Here we can see the key characteristics of the binary:

- **ELF 64-bit**: The file is in the **Executable and Linkable Format (ELF)**, the standard format for binaries on Linux. It is a **64-bit** file, meaning it requires a 64-bit operating system to be processed or executed.
- **LSB**: Stands for **Least Significant Byte** (little-endian). This specifies the "endianness" or byte-order used by
the CPU. This is the standard for x86 and x86-64 (Intel and AMD)
architectures.
- **relocatable**: This is a critical distinction. It means the file is an **object file** (e.g., `main.o`) rather than a finished program. It contains code and data suitable for **linking** with other object files to eventually create an executable, but it cannot be run by itself in its current state.
- **x86-64**: The target CPU architecture is the 64-bit version of the x86 instruction set (commonly used by Intel and AMD processors).
- **version 1 (SYSV)**: This indicates the file adheres to the **System V Application Binary Interface (ABI)** version 1, which is the base standard for how programs interact with the system.
- **BuildID[sha1]=...**: A unique cryptographic hash (SHA-1) generated during compilation. It is used to identify this specific build of the file, allowing developers
to match the binary with its corresponding debug symbols later.
- **with debug_info**: The file contains extra metadata (like variable names and line numbers) that allows tools like `gdb` to debug the code.
- **not stripped**: The file still contains its **symbol table** (a list of function and variable names). "Stripping" a file removes
this info to save space, but it makes the binary much harder to debug or analyse
