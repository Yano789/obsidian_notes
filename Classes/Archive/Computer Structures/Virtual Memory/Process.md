A **process** is a unit of work in the system. It is an active entity, with its states changing over time as the instructions are executed

![[Process-1.webp|514x445]]
*Sample Memory Allocation for a Single Process* 

Each Box above represents a *process' context or state*:
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



___
# Termination / exit() [[System Call (Trap)]]
- Orphaned
	- Parents terminate before child
	- Adopted by init/equivalent
- Zombies (when terminated, [[Operating System (OS)]] will [[Deallocate]] its [[Virtual Memory]] but keep its metadata until parent [[Process]] calls *wait()/waitpid()*)
	- Once parent calls wait, the [[Classes/Computer System Engineering/The Computer System/Operating System (OS)/Kernel/Kernel|Kernel]] will remove the zombie child and unassign the pid ([[Process]] ID)
	- Dead Children
	- Parents don't know yet

