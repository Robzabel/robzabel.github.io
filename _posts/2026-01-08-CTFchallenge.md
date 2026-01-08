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

### Reconnaissance 
Since this is not an executable file, it wont run in my environment. Therefore, I will spawn the challenge docker image and connect to the server through net cat, using the provided IP address and port number.

Once on the Docker instance, I ran a few commands to search around and see if there was anything interesting to find. After a while of looking through directories, there was nothing jumping out at me so I decided to Google the Diamorphine root kit. I found that is is a GitHub project by m0nad - [text](https://github.com/m0nad/Diamorphine/tree/master)
As the README explains “*the module starts invisible, to remove you need to make it visible”.*  The functionality of the rootkit is utilised by entering process kill commands with the following signals:

- Hide/unhide any process by sending a signal 31;
- Sending a signal 63(to any pid) makes the module become (in)visible;
- Sending a signal 64(to any pid) makes the given user become root;
- Files or directories starting with the MAGIC_PREFIX become invisible;

On the docker image I tested the commands with varying success:

*kill -31 5*, hid the process with the PID of 5
*kill -64 0*, elvated me to a root shell
*kill -63 0*, caused kernel panic and crashed the system

I looked at the source code of the rootkit on github. In the directory, there is a header file and a C source file. In the header file I found where the variables are defined for SIGINVIS, SIGSUPER, SIGMODINVIS:
![_config.yml]({{ site.baseurl }}/images/headerFile.png)
By searching the C code file for the signal number variable names, I was able to find that they are referenced in the hacked_kill function:
![_config.yml]({{ site.baseurl }}/images/sourceFile.png)
I opened the kernel module file up in Ghidra and located the hacked_kill function, where the comparisons (CMP) instructions can be seen in the assembly code:
![_config.yml]({{ site.baseurl }}/images/Ghidra.png)
Using Ghidra’s unit converter function, I changed the hex notation to decimal and found that SIGINVIS = 31, SIGSUPER = 64, but the number required for SIGMODINVIS is actually 46.

### Getting the Flag

I logged back onto the box and elevated to a root shell (changing the prompt from $ to #), made the root kit visible, then entered the uninstall command from the README.
![_config.yml]({{ site.baseurl }}/images/finalConsole.png)
Now that the Rootkit has been stopped all files that were hidden using the MAGIC_PREFIX are now visible, so now its a case of checking the directories for a flag.txt file. I started listing the directories in the root until I got to /opt in which I found a directory called psychosis, in here was the the flag.