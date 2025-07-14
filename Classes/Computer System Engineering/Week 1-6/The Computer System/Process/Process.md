---
aliases:
  - processes
---
A **process** is a unit of work in the system. It is an active entity, with its states changing over time as the instructions are executed

![[Classes/Archive/Computer Structures/Photos/Process-1.webp|284x284]]
*Sample Memory Allocation for a Single Process* 

Each Box above represents a *process' context*:
1. **Text**: Code or Instructions
2. **Value of Program Counter (PC)**
3. **Contents of the processors register**
4. **Dedicated Address Space** (block of location) in the memory
5. [[Stack Implementation|Stack]] (temporary data)
6. **Data** (allocated memory during compile time; global and static variables)
7. **Heap** (dynamically allocated memory)
___
# Process ID (pid)
an integer used to identify each process, unique in the system

___
# Concurrency and Protection
the two abstractions of a process

## Protection
- Each process runs in a different address space and sees itself running in a virtual machine
- They think they are the only process running
- Each process is managed by the [[Scheduling and Multiple Interrupts|Kernel Scheduler]] 

## Concurrency
- Mutliple processes being in progress at the same time, sharing system resources
- [[Timesharing]]/[[Mulitprogramming]]

___
# Piggybacking
- The process can *piggyback* on the [[System Call (Trap)]] to get access to the [[Kernel Mode (PC31 MSB = 1)|kernel mode]]

___
# Process Management
## Process Scheduling States
1. **New**: *Created* process
2. **Running**: Instructions are *being executed*
3. **Waiting**: The process is *waiting for an event* to continue
4. **Ready**: The process is *waiting to be assigned* to a processor
5. **Terminated**: The process has *finished execution*

![[Process-4.webp|359x261]]

## Process Table
- a data structure containing all sorts of information about current process in the system
- It is maintained by the [[Classes/Computer System Engineering/Week 1-6/The Computer System/Operating System (OS)/Kernel/Kernel|Kernel]] to facilitate [[Context Switching|context switching]] and [[Scheduling and Multiple Interrupts|scheduling]].
- made up of an array of [[Process#Process Control Block (PCB)|Process Control Blocks (PCB)]]  


## Process Control Block (PCB)
- also known as **Task Control Block (TCB)**
- stores each process' metadata:
	- [[Process#Process Scheduling States|Process Scheduling State]]
	-  Program Counter (PC) - address for the next instruction
	- CPU Registers - [[Stack Implementation]]
	- [[Scheduling and Multiple Interrupts|Scheduling Information]]
	- Memory Management Information
	- Accounting Information - amount of CPU and real time used, time limits, accounting numbers, [[Process#Process ID (pid)]] 
	- [[Device Controllers#I/O]] status

## Process Scheduling Detail
- selects an available process for [[Program]] execution on the CPU
	- **single-processor system**: 
		- there will never be more than one actual running process at any instant
		- if there are more, they will have to wait in the queue

### Process Scheduling Queues
1. **Job** Queue - all processes in the system
2. **Ready** Queue - all processes residing in main memory, ready and waiting to be executing
3. **Device** Queue - all processes waiting for an [[Device Controllers#I/O]] device (*one queue for each device*)

Each queue contains a pointer to the corresponding [[Process#Process Control Block (PCB)]] that are waiting for either CPU or [[Device Controllers#I/O]] 
___
# Process Operations
## Process Creation
We can create new processes using [[fork()]] [[System Call (Trap)]] 
1. The process creator is called a **Parent Process**, the new processes are called the *children* of that process
	- The child process inherits all the address space (includes state) of the original parent process at the point of [[fork()]]
	- They operate in different address spaces and thus work [[Process#Concurrency|concurrently]]
	- The parent will wait for the child to [[wait()]] to read the child process' exit status, only then will the [[Process#Process Control Block (PCB)|PCB]] be removed
2. Each of these processes may create more **Child Processes** forming a tree of processes

### Process Tree
P0 (Parent process) creates 3 child processes, and one child process creates another child process
![[Classes/Computer System Engineering/Week 1-6/The Computer System/Process/Process-1.webp|284x284]]


![[Process-2.webp|350]]

> [!NOTE] The pid variable of the parent is the actual pid of the child, HOWEVER, the pid variable of the child is 0


![[Process-3.webp|411x279]]

**Parent**
- [[fork()]] to create a child and [[wait()]] for it to [[exit()]] to continue

**Child**
- gets created by parent [[fork()]] and will run until [[exit()]]

## Process Termination
resources for processes are limited, thus we must kill/[[exit()]] processes to save or reuse these resources

### Orphaned Processes
- Parents terminate before child
- Adopted by init/equivalent

### Zombie Processes
- when terminated, [[Operating System (OS)|OS]] will [[Deallocate]] its [[Virtual Memory]] but keep its metadata until parent process calls *[[wait()]]
- Once parent calls [[wait()]], the [[Classes/Computer System Engineering/Week 1-6/The Computer System/Operating System (OS)/Kernel/Kernel|Kernel]] will remove the zombie child and unassign the [[Process#Process ID (pid)]]
- Parents don't know that the child is dead yet
- *Zombie Processes take up one bit for pid in the [[Process#Process Control Block (PCB)]] so we need to get rid of it to run more processes* 

___
# Asynchronous Processing
- running Processes without waiting for others to finish ([[System Call (Trap)#Non-Blocking]])
- often used for [[Device Controllers#I/O]] operations
>[!NOTE] Asynchronous Processing does not necessarily require multi-threading


# Concurrent Processing
running multiple processes over time using [[Quanta]]
> [!NOTE] Concurrency needs asynchronous and multi-threading


# Parallel Processing
performing multiple tasks simultaneously 
>[!NOTE] Requires multiple processors/cores
