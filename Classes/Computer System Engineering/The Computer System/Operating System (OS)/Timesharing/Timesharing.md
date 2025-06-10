**Goal**: Provide interactive user experience and fast response times.

Naturally, [[Mulitprogramming]] allows for **timesharing**. Therefore it is **an extension** by allows multiple people to use the system at the same time. We do this by slicing the CPU into multiple time slices, [[Quanta]].

**Simplified implementation**:
- The [[Operating System (OS)]] maintains a list of active user [[Process|processes]].
- The CPU scheduler allocates a fixed time slice to each process in a **round-robin fashion**.
- If a process’s time slice expires, the CPU **switches to the next process** in the queue.
- Processes that need I/O or user input can be [[Interrupt|interrupted]] and put into a waiting state, allowing other [[Process|processes]] to use the CPU.
- For example in the diagram below, the CPU will run each job for a fixed [[Quanta]] `t` and switch to another (ready) job once that time slice ends:

![[Timesharing-1.webp]]