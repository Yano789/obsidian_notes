![[Classes/Archive/Computer Structures/Virtual Machine/Kernel|Kernel]]

The kernel is the **heart** of the [[Operating System (OS)]]
- it runs on the *physical space*, therefore it only knows [[Physical Address (PA)|physical addresses]]
- is a collection of code containing interrupts and handlers for a variety of situations

3 Ways to access kernel mode:
1. Reset
2. Supcall/[[System Call (Trap)]] *Software*
3. [[Asynchronous Interrupt]] *Hardware*
___
## Types of Privileges
[[Kernel Mode (PC31 MSB = 1)]]
[[User Mode (MSB = 0)]]

___
## Roles of the Kernel
### 1. Resource Allocator and Coordinator: Interrupt Driven I/O Operations
2 Types of Interrupts:
1. [[System Call (Trap)|Software Interrupt]]
2. [[Asynchronous Interrupt|Hardware Interrupt]] 

### 2. Security and Protection
- [[Reentrancy Kernel]] - Concurrent processes 
- [[Preemption Kernel]] - Interrupt to run the highest priority tasked
Kernel provides **defensive security measures**, protecting itself against internal or external attacks
1. Identify Users
2. Associate users with files and processes

### 3. Memory Management
#### [[Virtual Memory]] Implementation
1. **Support** [[Demand Paging]] Protocol
2. **Keep Track** of which parts of memory are currently being used and by whom
3. **Decide** which [[Process|processes]] to move in and out
4. **Mapping** files into process address space
- **[[Allocate]]** and **[[Deallocate]]** memory space as needed
    - If RAM is full, **migrate** some contents (e.g: least recently used) onto the **[[Swap Space]]** on the disk
- **Manage** the **[[Page Table]]** and any operations associated with it.

*Note: CPU caches are managed by the hardware (cache replacement policy, determining a HIT or a MISS * 

#### Configuring the [[Memory Management Unit (MMU)]]
Data transfer from disk to memory and vice versa is usually controlled by the **kernel** *(requires context switching)*, while data transfer from CPU registers to CPU [[The Cache Idea|cache]] is usually a **hardware function** without intervention from the kernel. There is too much [[Overhead]] if the kernel is also tasked to perform the latter.

Recall that the Kernel is responsible to program and set up the cache and [[Memory Management Unit (MMU)]] hardware, and manage the entire virtual memory. Kernel memory management routines are **triggered** when processes running in user mode encounter **page-fault** related interrupts. Careful **selection** of the page size and of a replacement policy can result in a greatly increased performance.

##### Cache Effective Access Time
We can compute the cache **effective access time as**:
$$
\alpha\tau + (1-\alpha) \times \epsilon
$$
where:
[[Cache Hit]] **ratio** $\alpha$, 
[[Cache Miss]] **access time** $\epsilon$ , and 
[[Cache Hit]] **access time** $\tau$ 
*Note: Cache Miss = $\alpha-1$*

### 4. Process Management
The kernel allows the system to support concepts that aim to improve the efficiency and responsiveness of the computer:
1. [[Mulitprogramming]]
2. [[Timesharing]] 

#### Key Differences

| **Feature**          | [[Mulitprogramming]]                                | [[Timesharing]]                                    |
| :------------------- | :-------------------------------------------------- | :------------------------------------------------- |
| **Primary Goal**     | Maximize CPU utilization and throughput             | Provide responsive, interactive user experience    |
| **User Interaction** | Minimal, often non-interactive (batch processing)   | High, interactive user experience                  |
| **CPU Scheduling**   | Job-based, switches when I/O is needed              | Time-based, fixed time slices ([[Quanta]])         |
| **Response Time**    | Can be longer, not optimized for interactivity      | Short, optimized for user interaction              |
| **Implementation**   | Multiple jobs loaded in memory, CPU switches on I/O | Multiple user processes, rapid context switching   |
| **Examples**         | Early mainframe systems, batch processing           | Modern operating systems, interactive applications |
[[Mulitprogramming]] focuses on **maximizing CPU usage** by **running multiple jobs simultaneously**

[[Timesharing]] aims to **provide a responsive, interactive experience for multiple users** by rapidly switching between processes

#### Process Manager
- part of the kernel code
- may be called either when there's timed [[Interrupt]] by the timed interrupt handler or trap handler
- keeps track of the system-wide [[Process Table]]

Responsible for:
1. **Creation and Termination** of both user and system processes
2. **Pausing and Resuming** processes in the event of [[Interrupt]] or [[System Call (Trap)]]
3. **Synchrnizing** processes and provides communications between virtual spaces
4. Provide mechanism to handle deadlocks