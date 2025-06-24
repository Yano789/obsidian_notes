supported by special [[Atomic Operation#Atomic Instructions]] implemented at the **hardware level**, and requires integration with the [[Scheduling and Multiple Interrupts|Kernel Scheduler]]. It will put the requesting [[Thread]]/[[Process]] to sleep if the lock has already been acquired by another

>[!WARNING]
>It is **expensive** to put [[Thread]] to sleep then wake them up again. Plus, they need a lot of [[Overhead]] because of the [[Scheduling and Multiple Interrupts|Kernel Scheduler]] 

>[!IMPORTANT]
You **NEED** to use a [[Condition Variable]] as a **signaling mechanism** with the mutex lock. 

With mutex locks alone, we cannot easily block a [[Process]] out of its [[Critical Section (CS)]] based on any arbitrary condition even when the mutex is available.