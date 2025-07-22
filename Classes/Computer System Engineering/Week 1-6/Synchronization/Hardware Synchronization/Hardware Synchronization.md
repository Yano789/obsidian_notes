We can solve the [[Critical Section (CS)]] Problem using hardware solutions. These solutions are based on **Hardware Locking** to protect the [[Critical Section (CS)]]. 

> [!NOTE]
> The number of hardware locks per system is **physically** limited

# Preventing Interrupts
only works in **single-core systems** and is **NOT** feasible in [[Multicore Programming]] because:
- Time consuming
- Affects system clocks
- Decreases efficiency

Can be done using [[Atomic Operation#Atomic Instructions]]