# CTF

## Challenge 1

### Recon

- We identified the security properties of the given program, with the help of the `checksec` tool.
- There was no canary protecting the return address and the stack has execution permission.

### Vulnerability

The program read a file (`mem.txt`), and in order to get the flag we needed to change which file the program read. The path to the file was kept in the variable meme_file. The only moment in the execution of the program in which the user intervenes is when he gets to give a text input, that will be kept in a 20 byte `buffer`.

We understood the vulnerability would be connected to said buffer, and could be exploited by creating a buffer overflow. If we wrote more than 20 characters a buffer overflow would occur. We knew we could wirte on the stack and change other variables and we knew `mem_file` was next to the `buffer` on the stack. So in order to access flag.txt we sent as the input something like "[20 characters to fill the buffer]flag.txt". This changed the variable `mem_file` to "flag.txt" and we found the flag - `flag{8df95b4dbd7681ec6e6688826ae6fd12}`.

## Challenge 2

### Recon

- Just like before, we identified the security properties of the given program, with the help of the `checksec` tool.
- There was no canary protecting the return address and the stack has execution permission, once again.

### Vulnerability

The difference this time in the program, was a new variable, `val`, an array of 4 characters. The program would only open the text file if the condition `if(*(long*)val == 0xfefc2122)` was met.

We identified the same opportunity to induce a buffer overflow, except this time the variables were in the following order in the stack: `buffer`->`val`->`mem_file`. So we used the Python script to send the input "[20 characters to fill the buffer][0x22][0x21][0xfc][0xfe]flag.txt". This way the condition was met and we changed the variable `mem_file` to "flag.txt", just like in the first challenge. Doing this we found the flag - `flag{031964c904407b7f31a925abe31d5d1f}`.

# SEED Labs

## Buffer Overflow Attack Lab (Set-UID Version)

### Task 1: Getting Familiar with Shellcode

- We were able to understand the shellcode and run the generated 32 bit binary that executed the shellcode.
- A shell was launched when executing the binary, as expected.

### Task 2: Understanding the Vulnerable Program

- We understood how the program had a buffer overflow vulnerability, since it was copying a 517 bytes buffer to a 100 bytes one. This opens the possibility to get a root shell 
- By using the `make` command, we compiled the vulnerable program with flags for turning off StackGuard and the non-executable stack protections and set it as a root owned Set-UID program.

### Task 3: Launching Attack on 32-bit Program (Level 1)
