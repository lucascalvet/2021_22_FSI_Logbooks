# CTF
## Challenge 1

### Recon

- We identified the security properties of the given program, with the help of the `checksec` tool.
- This program has some active protections, however it's a `NO PIE` program.  
- A `No PIE` application tells the loader which virtual address it should use (and keeps its memory layout quite static). Hence, attackers against this application know up-front how the virtual memory for this application is (partially) organized, including the stack.

### Vulnerability

The program loads the flag from a file to a global variable appropriately named `flag`. Shortly after that, in the source code appears the following line: `scanf("%32s", &buffer);`. This `scanf` would be a vulnerability by itself, but here it's coupled with a `printf` of that very same buffer, opening the possibility for a format string attack that prints the contents of any variable in the stack. This happens because the user can submit an input that can be evaluated as a command provided it is a format string like `"something%s"`, for example. The user is in control of the format string and can trick the `printf` function into printing the value of a variable whose address is pointed in the stack.

We knew that we could print the value of any variable provided we knew it's address, so we used `gdb` on the program to find out the address of the flag global variable (which happened to be `0x804c060`). Having that knowledge we launched our format string attack by sending the input "\x60\xc0\x04\x08%s". This printed the flag - `flag{7d1d4f6634c1f24af8b8ced952470bc6}`.

## Challenge 2

### Recon

- We identified the security properties of the given program, with the help of the `checksec` tool.
- This program has some active protections, however it's a `NO PIE` program.  
- A `No PIE` application tells the loader which virtual address it should use (and keeps its memory layout quite static). Hence, attackers against this application know up-front how the virtual memory for this application is (partially) organized, including the stack.

### Vulnerability

The difference this time in the program, was a new variable "val", an array of 4 characters. The program would only open the text file if the condition `if(*(long*)val == 0xfefc2122)` was met.

We identified the same opportunity to induce a buffer overflow, except this time the variables were in the following order in the stack: buffer->val->mem_file. So we used the Python script to send the input "[20 characters to fill the buffer][0x22][0x21][0xfc][0xfe]flag.txt". This way the condition was met and we changed the variable mem_file to "flag.txt", just like in the first challenge. Doing this we found the flag - `flag{031964c904407b7f31a925abe31d5d1f}`.


# SEED Labs
