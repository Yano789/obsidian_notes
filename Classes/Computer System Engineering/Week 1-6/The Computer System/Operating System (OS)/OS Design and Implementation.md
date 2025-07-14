---
tags: []
---
## User and System Goals
1. **User Goals**  - convenient, easy to learn, reliable, safe, fast
2. **System Goals** - easy to 1. design, 2. implement, 3. maintain. It should be flexible, reliable, error free, and efficient

## Policy and Mechanism Separation
*Note: Important for Flexibility*
1. **Policy** - what will be done
2. **Mechanism** - how to do it

### Benefits
1.  Flexibility
2. Modularity
3. Reusability
4. Ease of Updates

### Mechanism
low-level operations or [[Function|functions]] from the [[Operating System (OS)]] to do basic tasks. They define how the following are done:
- [[Context Switching]] - how the [[Operating System (OS)]] switches between different [[Process]] or threads
- [[Classes/Computer System Engineering/Week 1-6/The Computer System/Operating System (OS)/Kernel/Kernel#3. Memory Management|Memory Management]] - how memory is accessed, allocated, and deallocated
- [[Kernel Mode (PC31 MSB = 1)|File Management]] -how files are add, modified, and deleted
- **Synchronization Primitives** - how synchronous tools are implements

### Policy
high level strategies or rules that govern [[The Computer System]]. They define what should be done under certain conditions
- [[Scheduling and Multiple Interrupts]]
- [[Classes/Computer System Engineering/Week 1-6/The Computer System/Operating System (OS)/Kernel/Kernel#3. Memory Management|Memory Allocation Policy]]
- Access Control Policy
- Page Replacement Policy