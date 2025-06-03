---
aliases:
  - Shell
---
The [[Interpreter]] of UNIX Systems are known as shells

Users typically interact with a Unix Shell via a [[Terminal Emulator]], or by writing a shell script that contains a bunch of successive commands to be executed

# Common Shells
## Bourne-Again Shell (Bash)
Written as part of the GNU Project

## Z Shell (Zsh)
Relatively modern shell that is backwards compatible with bash

## Powershell
Object-oriented shell developed originally for Windows OS

# Two Ways to Implement Commands
 Built-In
- The command [[Interpreter]] itself contains the code to execute the command

[[System Programs]]
- typically found in default `PATH` such as `/usr/bin`

# Shell Main loop
![[Command-Line Interpreter-1.webp|511x301]]

*wait() refers to [[System Call (Trap)#Blocking|Blocking System Call]]*
- the wait() synchronizes 2 independent [[Process|processes]] 
- not all application requires parent to wait
- eg. [[Daemons]]