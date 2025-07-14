**Goal**: Increase CPU utilization and system throughput.

Multiprogramming involves running multiple programs (or [[Process|processes]]) **on a single processor system**, a concept that is needed for **efficiency**. The [[Operating System (OS)]] keeps several jobs in memory simultaneously. When one job waits for I/O operations to complete, the CPU can execute another job. This approach **maximizes CPU usage by reducing idle time.**

**Simplified implementation**:
- The [[Operating System (OS)]] maintains a **pool of jobs** in the job queue.
- **Jobs are selected** and loaded into memory.
- The CPU **switches between jobs** when they are waiting for I/O, ensuring that it is **always busy executing some job.**
- Jobs are executed until they are complete or require I/O operations, at which point **another job is scheduled.**

For example in diagram below, CPU will continue to run Job 3 **as long as** Job 3 does not `wait` for anything else.
    - When Job 3 waits for some I/O operation in the future, CPU will switch to READY jobs, e.g: either Job 1 or Job 2 (assuming Job 4 is still waiting then)

![[Mulitprogramming-1.webp]]