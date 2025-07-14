---
aliases:
  - POSIX Shared Memory
---
A region in the RAM that is created and shared among multiple [[Process|processes]] using [[System Call (Trap)|System Calls]] 

1. [[Classes/Computer System Engineering/Week 1-6/The Computer System/Operating System (OS)/Kernel/Kernel|Kernel]] [[Allocate|allocates]] and establishes a region of memory and return to the caller [[Process]]
2. Reading and writing is now possible without assistance from the [[Classes/Computer System Engineering/Week 1-6/The Computer System/Operating System (OS)/Kernel/Kernel|Kernel]]

![[Shared Memory-1.webp]]
