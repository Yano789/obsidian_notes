![[Classes/Archive/Computer Structures/Virtual Machine/Kernel|Kernel]]

The kernel is the **heart** of the [[Operating System (OS)]]
- it runs on the *physical space*, therefore it only knows [[Physical Address (PA)|physical addresses]]
- is a collection of code containing interrupts and handlers for a variety of situations

3 Ways to access kernel mode:
1. Reset
2. Supcall/[[System Call (Trap)]] *Software*
3. [[Asynchronous Interrupt]] *Hardware*
## Types of Privileges
### Kernel Mode (PC31 MSB = 1)
a specific privilege wherein the kernel has/can:
1. **SECURITY**: Ultimate access and control to all hardware in the computer system (mouse, keyboard, display, network cards, disk, RAM, CPU, etc)
2. **FILE MANAGEMENT**: Know (and lives in) the [[Physical Address (PA)]] space and manages the [[Memory Hierarchy]]
3. **RESOURCE ALLOCATION**: Receive and manage I/O requests and interrupt other [[Classes/Computer System Engineering/The Computer System/Operating System (OS)/User Program|user programs]] 
4. **PROCESS MANAGEMENT**: Manage other user program locations on the RAM, the [[Memory Management Unit (MMU)]], and schedule user program executions
**Kernel Mode** 
- needs *Kernel Code and Physical Address*
- has access to hardware

### User Mode(MSB = 0)
- All other [[Classes/Computer System Engineering/The Computer System/Operating System (OS)/User Program|user programs]] that run on a virtual machine
- Has access to *system calls* (supervisor calls) when they require services from the kernel
	- change mode to *kernel mode* $\rightarrow$ then back to *user mode* 
- needs [[Virtual Address (VA)]]
- no access to the hardware

## Roles of the Kernel
### Resource Allocator and Coordinator: Interrupt Driven I/O Operations
2 Types of Interrupts:
1. [[System Call (Trap)|Software Interrupt]]
2. [[Asynchronous Interrupt|Hardware Interrupt]] 

### Security
**Reentrancy Kernel**
allows multiple processes to be executing in the kernel mode **at any given point of time** (*concurrent*)

**Preemption Kernel**
allows the scheduler to **interrupt processes in Kernel Mode** to *execute the highest priority task* that are ready to run, thus enabling kernel functions to be interrupted as well

## Memory Management
### [[Virtual Memory]] Implementation
1. Support [[Demand Paging]] Protocol
2. Keep Track of which parts of memory are currently being used and by whom
3. Decide which processes to move in and out