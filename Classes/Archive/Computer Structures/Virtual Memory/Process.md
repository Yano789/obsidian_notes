A **process** is a unit of work in the system. It is an active entity, with its states changing over time as the instructions are executed

![[Process-1.webp|514x445]]
*Sample Memory Allocation for a Single Process* 

# Termination / exit() [[System Call (Trap)]]
- Orphaned
	- Parents terminate before child
	- Adopted by init/equivalent
- Zombies (when terminated, [[Operating System (OS)]] will [[Deallocate]] its [[Virtual Memory]] but keep its metadata until parent [[Process]] calls *wait()/waitpid()*)
	- Once parent calls wait, the [[Classes/Computer System Engineering/The Computer System/Operating System (OS)/Kernel/Kernel|Kernel]] will remove the zombie child and unassign the pid ([[Process]] ID)
	- Dead Children
	- Parents don't know yet