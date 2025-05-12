![[Classes/Archive/Computer Structures/Virtual Machine/Kernel|Kernel]]

The kernel is the **heart** of the [[Operating System]]
- it runs on the *physical space*, therefore it only knows [[Physical Address (PA)|physical addresses]]

## Kernel Mode (PC31 MSB = 1)
a specific privilege wherein the kernal has/can:
1. **Ultimate access** and control to all hardware in the computer system (mouse, keyboard, display, network cards, disk, RAM, CPU, etc)
2. Know (and lives in) the [[Physical Address (PA)]] space and manages the [[Memory Hierarchy]]
3. **Interrupt** other [[User Program]]
4. Receive and manage I/O requests
5. **Manage other user program** locations on the RAM, the [[Memory Management Unit (MMU)]], and schedule user program executions

## User Mode(MSB = 0)
- All other [[User Program]] that run on a virtual machine
- Has access to *system calls* (supervisor calls) when they require services from the kernel
	- change mode to *kernel mode* $\rightarrow$ then back to *user mode* 