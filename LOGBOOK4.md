# CTF

# SEED Labs

## Environment Variable and Set-UID Program Lab

### 1: Manipulating Environment Variables
 
- printenv or env are used to print environment variables
- export and unset are used to set and unset environment variables

### Task 2: Passing Environment Variables from Parent Process to Child Process

After compiling two versions of myprintenv.c, one with the printenv function call on the case 0 (child) and other on the default case of the switch statement, we wrote the output of both into two diferent log files. Finally, we conclude that the environment variables are inherited by the child process, by comparing both log files with the diff bash command and observing no differences. 
