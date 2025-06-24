A lock is re-entrant if it is **safe** to be acquired **again** by a caller that is already holding the lock.

# Reentrance Lockout
If you use a **non-reentrant lock** and try to acquire it again, you will experience a **reentrance lockout**

# Releasing Locks
>[!NOTE]
>For some locks, you must **release** the lock `N` times after **acquiring** it `N` times




*Related to [[Java Synchronization]]*
