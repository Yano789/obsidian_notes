---
aliases:
  - atomic
---
An indivisible operation that completes in a single step relative to other [[Thread]]. It appears instantaneous and is executed without any interference from other operations, ensuring consistency and preventing [[Race Condition|race conditions]]

> [!NOTE] Once an atomic operation begins, it will complete without interference

# Atomic Instructions
implemented set of atomic operations

>[!WARNING]
>Implementing atomic instructions **locks the memory bus**. Thus, [[Critical Section (CS)#Mutual Exclusion (MutEx)|mutual exclusion]] us trivial