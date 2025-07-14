---
aliases:
  - busy waiting
---
a simple variable that provides [[Critical Section (CS)#Mutual Exclusion (MutEx)|mutual exclusion]]

An attempt to `acquire()` the lock causes a [[Process]] or [[Thread|Thread]] to wait in a loop *("spin")* while checking whether the lock is available

>[!NOTE]
>This *busy waiting* wastes the caller's quantum until the caller acquires the lock to progress

Spinlocks waste CPU cycles by utilizing 100% CPU time of just waiting to check if the spinlock is available

>[!WARNING]
>Using this in a single-core CPU will cause your CPU to hang since your one core will wait forever

Hence, only use spinlocks when: 
1. you **KNOW** the anticipated waiting time is shorter than a [[Quanta|quantum]]
2. [[Multicore Programming]] is present and
3. No [[Context Switching]] is required