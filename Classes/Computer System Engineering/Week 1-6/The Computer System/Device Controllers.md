---
aliases:
  - Controllers
---

electronic components inside a computer that are in charge of specific devices:
1. Registers **(mini-cpu)**
2. Local Memory **Buffer** - stores hardware action
3. A program to communicate with the *device driver* **(translator)**
## Device Drivers
A specific program to *interpret* the behavior of each device type (translator between device and CPU)

Many drivers run in [[Classes/Computer System Engineering/Week 1-6/The Computer System/Operating System (OS)/Kernel/Kernel|kernel mode]] (may require reboot upon installation), but they may also run in *user mode* 

Running in *user mode* will be **slower** because they must switch between the *kernel mode* and the *user mode* frequently (**however, this is good** because if the code is wrong it wont overwrite the kernel memory)

## I/O
**Output:** *MOVE* data from the *device controller's buffer* to the *output device*
**Input:** *FROM* the *input device* to the *device controller's buffer* 