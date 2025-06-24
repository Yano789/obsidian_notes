allow a [[Process]] or [[Thread]] to wait for completion of a given **event** on a particular object

used to **communicate** between [[Process]] and [[Thread]] when certain conditions become `true`

>[!WARNING]
>Condition variables should **ALWAYS** be implemented with [[Mutex Lock|mutex locks]]. When implemented properly, they provide **condition synchronization**

# Waiting Loop
It is important to put the waiting of a [[Condition Variable]] in a `while` loop due to the possibility of:
1. **Spurious Wakeup** - a [[Thread]] waking up even if not one woke it up (happens for performance reasons)
2. **Extraneous Wakeup** - waking up [[Thread|threads]] that aren't scheduled
