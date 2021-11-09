# CTF

# SEED Labs

## Environment Variable and Set-UID Program Lab

### Task 1: Manipulating Environment Variables
 
- printenv or env are used to print environment variables
- export and unset are used to set and unset environment variables

### Task 2: Passing Environment Variables from Parent Process to Child Process

- Step 1, 2: After compiling and executing both myprintenv.c versions, we obtain ouputs with the environment variables.

- Step 3: After compiling two versions of myprintenv.c, one with the printenv function call on the case 0 (child) and other on the default case of the switch statement, we wrote the output of both into two diferent log files. Finally, we conclude that the environment variables are inherited by the child process via `fork()`, by comparing both log files with the diff bash command and observing no differences. 

### Task 3: Environment Variables and execve()

- Step 1: After compiling the myenv.c program nothing is outputed to the screen.

- Step 2: Adding the argument `environ` to the excve function, we obtain the environment variables as an ouput.

- Step 3: When the program is started by the `excve()` function call, in order to inherit the environment variables, the function has to be called with the eviron argument (pointer to array of pointers to strings, called the "environment").

###  Task 4: Environment Variables and system()

- When using the system function call with the argument "/usr/bin/env", we obtain the the environment varibales, proving the previous task 4 description. 

### Task 5: Environment Variable and Set-UID Programs

- When we created an environment variable,

### Task 6: The PATH Environment Variable and Set-UID Programs
