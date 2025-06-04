---
aliases:
  - Termination
  - terminate
tags:
  - ComputerSystemEngineering
---

## Termination [[System Call (Trap)|System Call]]
- Orphaned
	- Parents terminate before child
	- Adopted by init/equivalent
- Zombies (when terminated, [[Operating System (OS)]] will [[Deallocate]] its [[Virtual Memory]] but keep its metadata until parent [[Process]] calls *wait()/waitpid()*)
	- Once parent calls wait, the [[Classes/Computer System Engineering/The Computer System/Operating System (OS)/Kernel/Kernel|Kernel]] will remove the zombie child and unassign the [[Process#Process ID (pid)]]
	- Dead Children
	- Parents don't know yet