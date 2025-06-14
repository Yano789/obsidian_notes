mappings between the [[Threads#2. Kernel Level Threads|Kernel Level Threads]] and [[Threads#1. User Level Threads|User Level Threads]] 

# Types of Thread Mappings

## Many to One 
- many [[Threads#1. User Level Threads|User Level Threads]] to one [[Threads#2. Kernel Level Threads|Kernel Level Threads]] 

**Advantage**:
- Thread management is done by the thread library in user space, so it is more **efficient** as opposed to kernel thread management.
- Developers may create as many threads as they want
- Entire thread context-switching is maintained by the user-level thread library **entirely**

**Disadvantage**:
- **The entire process will block** if a thread makes a blocking system call since kernel isn’t aware of the presence of these user threads
- Since only one thread can access the kernel at a time, multiple threads attached to the same kernel thread are unable to run in parallel on multicore systems

![[Pasted image 20250614171649.webp]]

## One to One
- Maps **each** user thread to a kernel thread. You can simply think of this as process threads to be **managed** entirely by the Kernel.

**Advantage**:
- Provides **more concurrency** than the many-to-one model by allowing another thread to run when a thread makes a blocking system call.
- Allows **multiple** threads to run in parallel on multiprocessors.

**Disadvantage**:
- Creating a user thread requires creating the corresponding kernel thread (a lot of **overhead**, system call must be made)
- **Limited** amount of threads can be created to not burden the system
- **May** have to involve the kernel when there is a context switch between the threads (overhead)

![[Pasted image 20250614171904.webp]]

## Many to Many
**Multiplexes** many user-level threads to a smaller or equal number of kernel threads.

This is the best of both worlds:

- Developers can **create** as many user threads as necessary,
- The corresponding kernel threads can run in **parallel** on a multiprocessor.

![[Pasted image 20250614172003.webp]]

A variation of many-to-many mapping, the **two-level model**: both multiplexing user threads and allowing some user threads to be mapped to just one kernel thread.

![[Pasted image 20250614172013.webp]]