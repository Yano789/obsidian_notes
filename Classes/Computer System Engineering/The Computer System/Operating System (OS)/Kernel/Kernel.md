![[Classes/Archive/Computer Structures/Virtual Machine/Kernel|Kernel]]

The kernel is the **heart** of the [[Operating System (OS)]]
- it runs on the *physical space*, therefore it only knows [[Physical Address (PA)|physical addresses]]
- is a collection of code containing interrupts and handlers for a variety of situations

3 Ways to access kernel mode:
1. Reset
2. Supcall/[[System Call (Trap)]] *Software*
3. [[Asynchronous Interrupt]] *Hardware*

## Types of Privileges
[[Kernel Mode (PC31 MSB = 1)]]
[[User Mode(MSB = 0)]]

## Roles of the Kernel
### 1. Resource Allocator and Coordinator: Interrupt Driven I/O Operations
2 Types of Interrupts:
1. [[System Call (Trap)|Software Interrupt]]
2. [[Asynchronous Interrupt|Hardware Interrupt]] 

### Security
1. [[Reentrancy Kernel]]
2. [[Preemption Kernel]]

### 2. Memory Management
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
Data transfer from disk to memory and vice versa is usually controlled by the **kernel** *(requires context switching)*, while data transfer from CPU registers to CPU [[The Cache Idea|cache]] is usually a **hardware function** without intervention from the kernel. There is too much **overhead** if the kernel is also tasked to perform the latter.

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

### 3. Process Management
The kernel allows the system to support concepts that aim to improve the efficiency and responsiveness of the computer:
1. Mulitprogramming
2. Timesharing

##### Multiprogramming
**Goal**: Increase CPU utilization and system throughput.


#### Timesharing