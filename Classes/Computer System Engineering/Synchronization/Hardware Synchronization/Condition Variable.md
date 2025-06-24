allow a [[Process]] or [[Thread]] to wait for completion of a given **event** on a particular object

used to **communicate** between [[Process]] and [[Thread]] when certain conditions become `true`

>[!WARNING]
>Condition variables should **ALWAYS** be implemented with [[Mutex Lock|mutex locks]]. When implemented properly, they provide **condition synchronization**



