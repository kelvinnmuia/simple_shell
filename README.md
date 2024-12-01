# 0x16. C - Simple Shell 
## The Domains/Concepts covered in this project: `C` `Group project` `Syscall`

I built a simple Linux shell in C, implementing core functionalities such as command 
execution, argument parsing, and support for built-in commands like `cd` and `exit` using 
system calls like `execve`, `fork`, `wait`, `chdir`, and `read`. The shell handled input, managed 
processes, and supported error handling through functions like `perror` and `fflush`. This 
project demonstrated efficient use of system-level programming concepts and Unix system calls 
to replicate basic shell behavior.

## More Info
   **Output**
  * Unless specified otherwise, your program **must have the exact same output** as sh (/bin/sh) as well as the exact same error output.
  * The only difference is when you print an error, the name of the program must be equivalent to your argv[0] (See below)

Example of error with `sh`:

```
$ echo "qwerty" | /bin/sh
/bin/sh: 1: qwerty: not found
$ echo "qwerty" | /bin/../bin/sh
/bin/../bin/sh: 1: qwerty: not found
$
```

Same error with your program `hsh`:

```
$ echo "qwerty" | ./hsh
./hsh: 1: qwerty: not found
$ echo "qwerty" | ./././hsh
./././hsh: 1: qwerty: not found
$
```

## Compilation

The shell will be compiled this way:

```
gcc -Wall -Werror -Wextra -pedantic -std=gnu89 *.c -o hsh
```

## Testing

Your shell should work like this in interactive mode:

```
$ ./hsh
($) /bin/ls
hsh main.c shell.c
($)
($) exit
$
```

But also in non-interactive mode:

```
$ echo "/bin/ls" | ./hsh
hsh main.c shell.c test_ls_2
$
$ cat test_ls_2
/bin/ls
/bin/ls
$
$ cat test_ls_2 | ./hsh
hsh main.c shell.c test_ls_2
hsh main.c shell.c test_ls_2
$
```

## Tasks :page_with_curl:

**0. Betty would be proud**

Write a beautiful code that passes the Betty checks

  * [simple_shell](https://github.com/kelvinnmuia/simple_shell)

**1. Simple shell 0.1**

Write a UNIX command line interpreter.

  * Usage: `simple_shell`

Your Shell should:

  * Display a prompt and wait for the user to type a command. A command line always ends with a new line.
  * The prompt is displayed again each time a command has been executed.
  * The command lines are simple, no semicolons, no pipes, no redirections or any other advanced features.
  * The command lines are made only of one word. No arguments will be passed to programs.
  * If an executable cannot be found, print an error message and display the prompt again.
  * Handle errors.
  * You have to handle the “end of file” condition (`Ctrl+D`)

You don’t have to:

  * use the `PATH`
  * implement built-ins
  * handle special characters : `"`, `'`, `, `\`, `*`, `&`, `#`
be able to move the cursor
handle commands with arguments
`execve` will be the core part of your Shell, don’t forget to pass the environ to it…

```
julien@ubuntu:~/shell$ ./shell 
#cisfun$ ls
./shell: No such file or directory
#cisfun$ /bin/ls
barbie_j       env-main.c  exec.c  fork.c  pid.c  ppid.c    prompt   prompt.c  shell.c  stat.c         wait
env-environ.c  exec    fork    mypid   ppid   printenv  promptc  shell     stat test_scripting.sh  wait.c
#cisfun$ /bin/ls -l
./shell: No such file or directory
#cisfun$ ^[[D^[[D^[[D
./shell: No such file or directory
#cisfun$ ^[[C^[[C^[[C^[[C
./shell: No such file or directory
#cisfun$ exit
./shell: No such file or directory
#cisfun$ ^C
julien@ubuntu:~/shell$ echo "/bin/ls" | ./shell
barbie_j       env-main.c  exec.c  fork.c  pid.c  ppid.c    prompt   prompt.c  shell.c  stat.c         wait
env-environ.c  exec    fork    mypid   ppid   printenv  promptc  shell     stat test_scripting.sh  wait.c
#cisfun$ julien@ubuntu:~/shell$
```

  * [simple_shell](https://github.com/kelvinnmuia/simple_shell)

**2. Simple shell 0.2**

Simple shell 0.1 +

  * Handle command lines with arguments

  * [simple_shell](https://github.com/kelvinnmuia/simple_shell)

**3. Simple shell 0.3**

Simple shell 0.2 +

  * Handle the `PATH`
  * `fork` must not be called if the command doesn’t exist

```
julien@ubuntu:~/shell$ ./shell_0.3
:) /bin/ls
barbie_j       env-main.c  exec.c  fork.c  pid.c  ppid.c    prompt   prompt.c  shell_0.3  stat    test_scripting.sh  wait.c
env-environ.c  exec    fork    mypid   ppid   printenv  promptc  shell     shell.c    stat.c  wait
:) ls
barbie_j       env-main.c  exec.c  fork.c  pid.c  ppid.c    prompt   prompt.c  shell_0.3  stat    test_scripting.sh  wait.c
env-environ.c  exec    fork    mypid   ppid   printenv  promptc  shell     shell.c    stat.c  wait
:) ls -l /tmp 
total 20
-rw------- 1 julien julien    0 Dec  5 12:09 config-err-aAMZrR
drwx------ 3 root   root   4096 Dec  5 12:09 systemd-private-062a0eca7f2a44349733e78cb4abdff4-colord.service-V7DUzr
drwx------ 3 root   root   4096 Dec  5 12:09 systemd-private-062a0eca7f2a44349733e78cb4abdff4-rtkit-daemon.service-ANGvoV
drwx------ 3 root   root   4096 Dec  5 12:07 systemd-private-062a0eca7f2a44349733e78cb4abdff4-systemd-timesyncd.service-CdXUtH
-rw-rw-r-- 1 julien julien    0 Dec  5 12:09 unity_support_test.0
:) ^C
julien@ubuntu:~/shell$ 
```

  * [simple_shell](https://github.com/kelvinnmuia/simple_shell)

**4. Simple shell 0.4**

Simple shell 0.3 +

  * Implement the `exit` built-in, that exits the shell
  * Usage: `exit`
  * You don’t have to handle any argument to the built-in `exit`

  * [simple_shell](https://github.com/kelvinnmuia/simple_shell)

**5. Simple shell 1.0**

Simple shell 0.4 +

  * Implement the `env` **built-in**, that prints the current environment

```
julien@ubuntu:~/shell$ ./simple_shell
$ env
USER=julien
LANGUAGE=en_US
SESSION=ubuntu
COMPIZ_CONFIG_PROFILE=ubuntu
SHLVL=1
HOME=/home/julien
C_IS=Fun_:)
DESKTOP_SESSION=ubuntu
LOGNAME=julien
TERM=xterm-256color
PATH=/home/julien/bin:/home/julien/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
DISPLAY=:0
$ exit
julien@ubuntu:~/shell$ 
```

  * [simple_shell](https://github.com/kelvinnmuia/simple_shell)

**6. Simple shell 0.1.1**

Simple shell 0.1 +

  * Write your own `getline` function
  * Use a buffer to read many chars at once and call the least possible the `read` system call
  * You will need to use `static` variables
  * You are not allowed to use `getline`

You don’t have to:

  * be able to move the cursor

  * [simple_shell](https://github.com/kelvinnmuia/simple_shell)

**7. Simple shell 0.2.1**

Simple shell 0.2 +

  * You are not allowed to use strtok

  * [simple_shell](https://github.com/kelvinnmuia/simple_shell)

**8. Simple shell 0.4.1**

Simple shell 0.4 +

  * handle arguments for the built-in `exit`
  * Usage: `exit status`, where `status` is an integer used to exit the shell

```
julien@ubuntu:~/shell$ ./shell_0.4.1
$ exit 98
julien@ubuntu:~/shell$ echo $?
98
julien@ubuntu:~/shell$ 
```

  * [simple_shell](https://github.com/kelvinnmuia/simple_shell)

**9. setenv, unsetenv**

Simple shell 1.0 +

Implement the `setenv` and `unsetenv` builtin commands

  * `setenv`
    * Initialize a new environment variable, or modify an existing one
    * Command syntax: `setenv VARIABLE VALUE`
    * Should print something on stderr on failure
  * `unsetenv`
    * Remove an environment variable
    * Command syntax: `unsetenv VARIABLE`
    * Should print something on stderr on failure

  * [simple_shell](https://github.com/kelvinnmuia/simple_shell)

**10. cd**

Simple shell 1.0 +

Implement the builtin command `cd`:

  * Changes the current directory of the process.
  * Command syntax: `cd [DIRECTORY]`
  * If no argument is given to `cd` the command must be interpreted like `cd $HOME`
  * You have to handle the command `cd -`
  * You have to update the environment variable `PWD` when you change directory

  `man` `chdir`, `man getcwd`

  * [simple_shell](https://github.com/kelvinnmuia/simple_shell)

**11. ;**

Simple shell 1.0 +

  * Handle the commands separator `;`

```
alex@~$ ls /var ; ls /var
backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp
backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp
alex@~$ ls /hbtn ; ls /var
ls: cannot access /hbtn: No such file or directory
backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp
alex@~$ ls /var ; ls /hbtn
backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp
ls: cannot access /hbtn: No such file or directory
alex@~$ ls /var ; ls /hbtn ; ls /var ; ls /var
backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp
ls: cannot access /hbtn: No such file or directory
backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp
backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp
alex@~$
```

  * [simple_shell](https://github.com/kelvinnmuia/simple_shell)

**12. && and ||**

Simple shell 1.0 +

  * Handle the && and || shell logical operators

```
alex@~$ ls /var && ls /var
backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp
backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp
alex@~$ ls /hbtn && ls /var
ls: cannot access /hbtn: No such file or directory
alex@~$ ls /var && ls /var && ls /var && ls /hbtn
backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp
backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp
backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp
ls: cannot access /hbtn: No such file or directory
alex@~$ ls /var && ls /var && ls /var && ls /hbtn && ls /hbtn
backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp
backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp
backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp
ls: cannot access /hbtn: No such file or directory
alex@~$
alex@~$ ls /var || ls /var
backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp
alex@~$ ls /hbtn || ls /var
ls: cannot access /hbtn: No such file or directory
backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp
alex@~$ ls /hbtn || ls /hbtn || ls /hbtn || ls /var
ls: cannot access /hbtn: No such file or directory
ls: cannot access /hbtn: No such file or directory
ls: cannot access /hbtn: No such file or directory
backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp
alex@~$ ls /hbtn || ls /hbtn || ls /hbtn || ls /var || ls /var
ls: cannot access /hbtn: No such file or directory
ls: cannot access /hbtn: No such file or directory
ls: cannot access /hbtn: No such file or directory
backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  spool  tmp
alex@~$
```

  * [simple_shell](https://github.com/kelvinnmuia/simple_shell)

**13. alias**

Simple shell 1.0 +

  * Implement the `alias` builtin command
  * Usage: `alias [name[='value'] ...]`
    * `alias`: Prints a list of all aliases, one per line, in the form `name='value'`
    * `alias name [name2 ...]`: Prints the aliases `name`, `name2`, etc 1 per line, in the form `name='value'`
    * `alias name='value' [...]`: Defines an alias for each `name` whose `value` is given. If `name` is already an alias, replaces its value with `value`

  * [simple_shell](https://github.com/kelvinnmuia/simple_shell)

**14. Variables**

Simple shell 1.0 +

  * Handle variables replacement
  * Handle the `$?` variable
  * Handle the `$$` variable

```
julien@ubuntu:~/shell$ ./hsh
$ ls /var
backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  snap  spool  tmp
$ echo $?
0
$ echo $$
5104
$ echo $PATH
/home/julien/bin:/home/julien/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
$ exit 
julien@ubuntu:~/shell$ 
```

  * [simple_shell](https://github.com/kelvinnmuia/simple_shell)

**15. Comments**

Simple shell 1.0 +

  * Handle comments (`#`)

```
julien@ubuntu:~/shell$ sh
$ echo $$ # ls -la
5114
$ exit
julien@ubuntu:~/shell$ 
```

  * [simple_shell](https://github.com/kelvinnmuia/simple_shell)

**16. File as input**

Simple shell 1.0 +

  * Usage: `simple_shell [filename]`
  * Your shell can take a file as a command line argument
  * The file contains all the commands that your shell should run before exiting
  * The file should contain one command per line
  * In this mode, the shell should not print a prompt and should not read from `stdin`

  * [simple_shell](https://github.com/kelvinnmuia/simple_shell)

## Additional Project Resources

  * [Unix shell](https://en.wikipedia.org/wiki/Unix_shell)
  * [Thompson shell](https://en.wikipedia.org/wiki/Thompson_shell)
  * [Ken Thompson](https://en.wikipedia.org/wiki/Ken_Thompson)
  * [Everything you need to know to start coding your own shell](https://docs.google.com/document/d/1hGYSlk9VEs1CRJ8TqcRRZi3_XF15SYZcZv6zvDsrUdo/edit?usp=sharing)
