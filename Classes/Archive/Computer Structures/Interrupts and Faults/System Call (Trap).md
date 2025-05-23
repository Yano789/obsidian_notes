---
aliases:
  - Software Interrupt
---

Application requests to use the operating system, which switches the CPU into kernel mode (uses operating system code).

It's a **TRAP** because the application is trapping into the operating system


Sometimes the user processes are **blocked** simply because they require inputs from and [[Device Controllers#I/O|I/O Device]]  

**TRAPS** are software generated [[Interrupt|interrupts]] that transfer the mode of the program to [[Classes/Computer System Engineering/The Computer System/Operating System (OS)/Kernel/Kernel#Kernel Mode (PC31 MSB = 1)|Kernel Mode]]

*Note: always save state before going into kernel mode, that way you can always come back after*