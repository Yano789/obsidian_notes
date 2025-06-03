---
aliases:
  - System Utilities
tags:
  - review
---
provide a convenient environment for program development and execution
- run on [[User Mode(MSB = 0)]] just like any other user-level application
- when it requires the [[Classes/Computer System Engineering/The Computer System/Operating System (OS)/Kernel|Kernel]], they run [[System Programs]]

# Categories of System Programs

## Package Managers: File Management and Modification
Text editors such as `nano` and `vim`

package managers such as `brew`, `apt`, `pacman`


## Status Information
Ask the system for information:
- date
- time
- amount of available memory or disk space

## Programming-Language Support
[[Compiler]], [[Assembler]], Debuggers, and [[Interpreter]] for common programming languages are available. 
[[System Programs#Package Managers File Management and Modification|Package Managers]] such as `npm`, and `pip` may be installed for easier development

## Program Loading and Execution
After assembling and compiling, we must load the program into the memory so that it can be executed.

## Communications
create virtual connections among the system

## Background Services
constantly running system-programs known as *services, subsystems,* or *[[Daemons]]*
