viewed as a **generalized [[Mutex Lock]]**. It provides [[Critical Section (CS)#Mutual Exclusion (MutEx)|mutual exclusion]]. It is a high-level **software** solution that relies on [[Hardware Synchronization]]

It is an **integer variable** that is maintained in the [[Classes/Computer System Engineering/Week 1-6/The Computer System/Operating System (OS)/Kernel/Kernel|Kernel]], which represents the number of avaibale resources for the sharing [[Process]]

implemented at the [[Classes/Computer System Engineering/Week 1-6/The Computer System/Operating System (OS)/Kernel/Kernel|Kernel]] Level
- Thus, its execution requires the calling [[Process]] to switch to [[Kernel Mode (PC31 MSB = 1)|Kernel Mode]] via a [[System Call (Trap)]] 
- Upon the initialization, the semaphore **descriptor is inherited** across a [[fork()]]
- Can only be accessed through 2 standard [[Atomic Operation|atomic]] [[System Call (Trap)|System Call]] operations: [[wait()]] and `signal()`

>[!NOTE]
>`acquire()` is the same as [[wait()]], and `release()` is the same as `signal()`

A parent [[Process]] can 
1. create a semaphore,
2. open it
3. and [[fork()]]

>[!NOTE]
>The child [[Process]] **does not need to open the semaphore** and **can close the semaphore** if the application is finished with it

Thus, you need to destroy a semaphore after using it. Just like [[Shared Memory]]

# Binary Semaphore
integer value: `0` or `1`

# Counting Semaphore
integer value: between `0` to `N`

# Implementation
Whenever the [[Process]]/[[Thread]] need to [[wait()]], it **reduces the semaphore**
- if the current semaphore value is **negative**, it blocks itself
- The [[Process]]/[[Thread]] are then added to the **waiting queue** associated with that semaphore

When a [[Process]] is completed, it will call the `signal()` function, and one [[Process]] in the queue is resumed by using the `wakeup()` [[System Call (Trap)|System Call]]

>[!IMPORTANT]
>We do not [[Spinlock|busy wait]] in the [[Critical Section (CS)]] of the [[Program]], we **ONLY** [[Spinlock|busy wait]] in the **[[Critical Section (CS)]] of the semaphore** 

This allows the [[Spinlock|busy waiting]] to be acceptable and still efficient
