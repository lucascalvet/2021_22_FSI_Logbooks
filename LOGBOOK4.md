# CTF

## Recon

- We identified the Wordpress version (5.8.2) in the following html element: `<meta name="generator" content="WordPress 5.8.2" />`
- In the following meta tag, we identified that the WooCommerce plugin (5.7.1) was being used (`<meta name="generator" content="WooCommerce 5.7.1" />`). This plugin is loaded from `/wp-content/plugins/woocommerce`.
- We identified two registered users - admin and orval_sanford (aka Orval Sanford) - by looking at the Recent Comments on the sidebar. Orval Sanford's username was identified by looking at the link when clicking in his name (`/author/orval_sanford/`), which then redirects to `/shop/`. These were verified to be users by inputting them in the login box with a random password and looking at the error message.

## Vulnerability

We were hinted that the exploitable vulnerability lied in the WooCommerce plugin, since the used WordPress version was the most recent one at the time. As such, we searched in exploit-db for WooCommerce exploits and discovered an exploit based on CVE-2021-34646. We confirmed this was the exploitable CVE in this case, by testing the flag `flag{CVE-2021-34646}` in the Week 4 - Challenge 1, which was accepted.

We researched the identified vulnerability, to understand that the problem was caused due to the generation of a verification link, which would be sent by email, that allows to directly authenticate as any user. The generation of this link would be triggered by sending a request to the home URL with the `wcj_user_id` parameter set to the corresponding user ID. Usually, the user ID of 1 corresponds to an administration account. By accessing `/wp-json/wp/v2/users/` we were able to verify that in fact the admin account has an user ID of 1. The generated link had a format like `/my-account/?wcj_verify_email=json_info` where `json_info` is a Base64 encoded JSON string containing the user ID and the generated hash for verification. However, this hash was simply an md5 encoding of the current time, which is easily guessed.

To exploit this vulnerability, we used the already made [exploit](https://www.exploit-db.com/exploits/50299) in the Exploit Database. This exploit generates three different verification links, based in three different timestamps, to maximize the possibility of a correct one. After trying different links we eventually succeded in authenticating as the admin account.

The flag - `flag{9ee3ba67c983ad1fdabd0a4635609f0a}` - was found in the first Post in `/wp-admin/edit.php`.


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

- We created three environment variables in the parent process (shell) and when we ran the setUID program almost all were inherited by the child process (program), except from `LD LIBRARY PATH`. After doing a research, we conclude that this environment variable is not inherited by setUID processes, because of security reasons, since it is the path which the linker should look in to, while linking dynamic libraries, or shared libraries.

### Task 6: The PATH Environment Variable and Set-UID Programs

- After setting our malicious code that created a new environment variable, as a setUID program and then checked the environment variables, we saw that the one we had created did not exist. After a dedicated search we conclude the environment in POSIX is inherited by child processes (created by fork call). However, when there are changes to the environment in the child process, those changes are not maintained in the parent process, when the child process terminates.
