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

