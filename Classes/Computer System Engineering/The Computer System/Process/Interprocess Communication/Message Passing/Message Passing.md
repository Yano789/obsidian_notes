[[Process|processes]] must communicate and synchronize their actions without sharing the same address space (this is done using the [[Classes/Computer System Engineering/The Computer System/Operating System (OS)/Kernel/Kernel|Kernels]] help

Message Passing has 2 Interfaces

# Sockets
A socket is one endpoint of a **two way communication link** between two programs

![[Pasted image 20250614162827.webp]]
![[Pasted image 20250614162928.webp]]
Steps:
1. P1 (server) makes a system call to create a socket
2. Kernel creates a **listening** socket and bind P1 to it
3. P2 (client) makes a system call to create and connect to an existing socket (called a connected socket)
4. Kernel creates a new communication socket between P1 and P2 (called an accepted socket)
5. P1 and P2 can communicate via the established socket (accepted socket in P1’s side and connected socket in P2’s side) in step 4 using `write` and `read` system calls

## Types of Sockets
1. **Listening** socket: Created by P1 and used to listen for incoming connections.
2. **Accepted** socket: Created by the kernel when P1 accepts the connection from P2, used for communication.
3. **Connected** socket: Created by P2 and used to establish a connection to the server and for communication.

# Message Queue
A queue data structure is maintained by the [[Classes/Computer System Engineering/The Computer System/Operating System (OS)/Kernel/Kernel|Kernel]] 
![[Pasted image 20250614163825.webp]]

# Socket vs Message Queue
Socket: Phone Calls
Message Queue: Mailbox