2 basic synchronization idioms:
1. **Synchronized Methods**
2. **Synchronized Statements**

Each object has an associated binary lock:
- `acquired` by invoking a synchronized method/block
- `released` by exiting a synchronized method/block

>[!NOTE] 
>Java Binary Lock guarantees [[Critical Section (CS)#Mutual Exclusion (MutEx)|mutex]] for an object's **method**

[[Thread|Threads]] waiting to acquire the lock are in the *entry set*. They are `blocked`, and they will only be `runnable` when they acquire the lock

Each object only **has one lock** per synchronized methods

# Java Static Lock
declaring *static methods* as synchronized creates:
- **1 lock** for the method
- **1 class lock** for each class

>[!WARNING]
>Class locks have their own queue set. Thus for each java class, there can be **multiple object locks** but only **1 class lock**

# Java Condition Synchronization
uses [[wait()]] and `notify()` methods as well as [[Condition Variable|condition variables]]