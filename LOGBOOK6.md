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

This time the only way we could access the `flag.txt` file was via a bash. The problem was that to launch said bash we needed to satisfy the condition `if(key == 0xbeef)`, and at first glance there wasn't any way to change the value of the `key` variable. But upon further analysis, we identified, once again, the format string vulnerability in the `scanf("%32s", &buffer);`/ `printf(buffer);` combo. The only type of format string attack that can change the value of a variable is the one that uses the formatting option `%n`. This option doesn't print anything, but the number of characters written is stored in the pointed location. This opens up a possibility to change the `key`.

In order to obtain the flag, we needed to change `key` to `0xbeef`. As we are using the `%n` option in our attack, we need to send an input that starts by the address of the `key` variable (after using gdb we found it to be `0x804c034`) and write `0xbeef` characters, or in decimal, 48879 characters. We used the python script to send an input with padding to wirte all the necessary characters, with a structure like this "aaaa\x34\xc0\x04\x08%48871x%n" (the starting characters are just there as the argument to be consumed by the padding). Running said script opened the bash, which in it's turn (using `cat < flag.txt`) allowed us to reach the flag - `flag{13107049574ad6c1dffec227ae128e62}`.


# SEED Labs
