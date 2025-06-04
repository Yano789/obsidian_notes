A **process** is a unit of work in the system. It is an active entity, with its states changing over time as the instructions are executed

![[Process-1.webp|514x445]]
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
# Concurrency and Protection
the two abstractions of a [[Process]]

## Protection
- Each [[Process]] runs in a different address space and sees itself running in a virtual machine
- They think they are the only process running
- Each [[Process]] is managed by the [[Scheduling and Multiple Interrupts|Kernel Scheduler]] 

## Concurrency
- Mutliple processes being in progress at the same time, sharing system resources
- [[Timesharing]]/[[Mulitprogramming]]

___
# Piggybacking
- The process can *piggyback* on the [[System Call (Trap)]] to get access to the [[Kernel Mode (PC31 MSB = 1)|kernel mode]]

___
# Process Management
## Process Scheduling States
1. **New**: *Created* [[Process]]
2. **Running**: Instructions are *being executed*
3. **Waiting**: The [[Process]] is *waiting for an event* to continue
4. **Ready**: The [[Process]] is *waiting to be assigned* to a processor
5. **Terminated**: The [[Process]] has *finished execution*

![[Process Management-1.png|359x261]]

## Process Table
- a data structure containing all sorts of information about current [[Process|processes]] in the system
- It is maintained by the [[Classes/Computer System Engineering/The Computer System/Operating System (OS)/Kernel/Kernel|Kernel]] to facilitate [[Context Switching|context switching]] and [[Scheduling and Multiple Interrupts|scheduling]].
- made up of an array of [[Process#Process Control Block (PCB)|Process Control Blocks (PCB)]]  


## Process Control Block (PCB)
- also known as **Task Control Block (TCB)**
- stores each [[Process|process']] metadata:
	- [[Process#Process Scheduling States|Process Scheduling State]]
	-  Program Counter (PC) - address for the next instruction
	- CPU Registers - [[Stack Implementation]]
	- [[Scheduling and Multiple Interrupts|Scheduling Information]]
	- Memory Management Information
	- Accounting Information - amount of CPU and real time used, time limits, accounting numbers, process id (pid)
	- [[Device Controllers#I/O]] status

## Process Scheduling Detail
- selects an available [[Process]] for [[Program]] execution on the CPU
	- **single-processor system**: 
		- there will never be more than one actual running [[Process]] at any instant
		- if there are more, they will have to wait in the queue

### Process Scheduling Queues
1. **Job** Queue - all [[Process|processes]] in the system
2. **Ready** Queue - all [[Process|processes]] residing in main memory, ready and waiting to be executing
3. **Device** Queue - all [[Process|processes]] waiting for an [[Device Controllers#I/O]] device (*one queue for each device*)

Each queue contains a pointer to the corresponding [[Process#Process Control Block (PCB)]] that are waiting for either CPU or [[Device Controllers#I/O]] 
___
# Process Operations
## Process Creation
We can create new [[Process|processes]] using [[Fork()]] [[System Call (Trap)]] 
1. The [[Process]] creator is called a **Parent Process**, the new [[Process|processes]] are called the *children* of that [[Process]]
2. Each of these [[Process|processes]] may create more **Child Processes** forming a tree of [[Process|processes]]

### Process Tree
![[Process-1.png|236x246]]
___
## Termination / exit() [[System Call (Trap)|System Call]]
- Orphaned
	- Parents terminate before child
	- Adopted by init/equivalent
- Zombies (when terminated, [[Operating System (OS)]] will [[Deallocate]] its [[Virtual Memory]] but keep its metadata until parent [[Process]] calls *wait()/waitpid()*)
	- Once parent calls wait, the [[Classes/Computer System Engineering/The Computer System/Operating System (OS)/Kernel/Kernel|Kernel]] will remove the zombie child and unassign the pid ([[Process]] ID)
	- Dead Children
	- Parents don't know yet

