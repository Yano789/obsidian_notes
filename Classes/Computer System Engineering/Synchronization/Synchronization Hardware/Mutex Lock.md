supported by special [[Atomic Operation#Atomic Instructions]] implemented at the **hardware level**, and requires integration with the [[Scheduling and Multiple Interrupts|Kernel Scheduler]]. It will put the requesting [[Threads]]/[[Process]] to sleep if the lock has already been acquired by another

>[!WARNING]
>It is **expensive** to put [[Threads]] to sleep then wake them up again. Plus, they need a lot of [[Overhead]] because of the [[Scheduling and Multiple Interrupts|Kernel Scheduler]] 
