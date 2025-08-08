>[!Important] Definition
>A socket is an endpoint for sending or receiving data across a computer network. It is a combination of an IP address and a port number, which together identify a specific process on a specific machine.
>
>Sockets serve as the programming interface between the **application** layer and the **transport** layer. They provide a mechanism for applications to send and receive data over the network using the services provided by the transport layer.

There are two types of sockets:

- **Stream Sockets (TCP)**: Used for connection-oriented communication. They provide reliable, ordered, and error-checked delivery of data.
- **Datagram Sockets (UDP)**: Used for connectionless communication. They provide a faster, but less reliable, delivery of data without guaranteeing order or error-checking.

![[Socket.png]]

From the diagram above, you can see that a socket is like a _door_ between application process and end-end transport layer protocol.

# Characteristics
A socket is one endpoint of a **two-way communication link** between two programs running on the network with the help of the **kernel**.

A single socket connection **typically** facilitates communication between two processes, but we may also enable socket sharing to enable communication among multiple processes (out of syllabus).

A socket has a **unique identifier**: IP address + PORT number, made up of 16 bit unsigned integer. We typically use **internet sockets** (used for network communication). There are also [file sockets](https://natalieagus.github.io/50005/ns/08-app-layer#file-sockets), but the details is out of syllabus. Socket is an application layer protocol. Note that IP is network layer protocol. You cannot create two sockets with the same identifier.

A socket is associated with an application. An application has to bind and listen to the socket.

>[!Important] Socket Binding
>Socket binding is the process of **associating** a socket with a specific IP address and port number on a host. Read the [appendix](https://natalieagus.github.io/50005/ns/08-app-layer#about-socket-binding) to find out more about socket binding if you’re interested.

In UNIX system, a socket is a special kind of file descriptor, similar to how we allow processes to open file descriptors to perform I/O operations.

For example, you can send a **HTTP** message to google.com server by putting the following in packet header:

- IP address: 216.58.221.78
- Port Number: 80 (for HTTP protocols)

> [!Note] 
> A port number is **specific** to transport layer protocol, mainly TCP and UDP which we will learn later. The **usage** and **interpretation** of the port number depend on the transport layer protocol (such as TCP or UDP) being used. See [practical examples](https://natalieagus.github.io/50005/ns/08-app-layer#practical-examples-of-port-usage) in appendix below to find out more.

# Socket API

The Socket API provides a set of functions for network communication in programming. It allows developers to create and manage network connections between processes on different machines (using internet sockets) or on the same machine (using UNIX domain sockets). Below is an overview of the key concepts and functions provided by the Socket API:

![[Socket-1.png]]