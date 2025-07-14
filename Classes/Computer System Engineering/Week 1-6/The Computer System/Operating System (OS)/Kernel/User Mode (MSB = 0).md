---
aliases:
  - User Mode
---

-  All other [[Application (User) Program|user programs]] that run on a virtual machine
- Has access to *system calls* (supervisor calls) when they require services from the kernel
	- change mode to *kernel mode* $\rightarrow$ then back to *user mode* 
- needs [[Virtual Address (VA)]]
- no access to the hardware