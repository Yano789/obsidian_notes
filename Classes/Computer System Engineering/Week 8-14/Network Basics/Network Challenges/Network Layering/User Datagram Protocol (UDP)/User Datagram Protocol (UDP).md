---
aliases:
  - UDP
---

UDP is a **connectionless** protocol that provides a simple and lightweight method for transmitting data [[Packets]] between devices. Unlike [[Transmission Control Protocol (TCP)]], UDP does not guarantee delivery or order of packets, making it faster but less reliable. It is commonly used for real-time applications like video streaming and online gaming.

UDP is also known as connectionless protocol. This protocol provides an unreliable-but-fast, may-be-out-of-order transfer of bytes between client and server.

Each datagram (packet) is sent independently, with no guarantee of order, delivery, or error correction. There is no handshake process; packets are simply sent to the destination without prior arrangement.

Like UDP, the series of instructions that handle UDP **exists as part of the Kernel**. The general API for UDP is as shown below:

![[User Datagram Protocol (UDP).png]]

- UDP socket is identified by 2-tuple only: IP and Port #
- In UDP, the client does not form a connection with the server like in TCP and instead just sends a datagram: attaches destination IP address and Port # to each packet
- Similarly, the server does not need to accept a connection and create a new socket like in TCP.
    - Instead, it just waits for (any) datagram(s) to arrive from (any) clients: extracts sender’s IP address and port# from received packet
- Transmitted data using UDP may be lost or received out-of-order.