---
aliases:
  - TCP
---

TCP is a **connection-oriented** protocol that ensures reliable and ordered delivery of data [[Packets]] between devices. It manages data transmission, flow control, congestion control, and error detection through mechanisms such as acknowledgments, retransmissions, and sequencing.

TCP provides reliable, in-order byte-stream transfer (“pipe”) between client and server in application viewpoint. It involves a three-way handshake process to establish a connection, ensuring that both parties are ready to communicate.

In terms of TCP implementation in UNIX-like systems, the series of instructions that handle TCP **exists as part of the Kernel**. For example, the Linux kernel is aware of the existence of network hardwares in the system and abstracts it into a set of link adapters. The TCP/UDP/IP stack is then aware of these adapters. They are further abstracted into higher-level concepts for users to use (via system-calls), such as the Socket API.

![[Transmission Control Protocol (TCP).png]]

- TCP Socket is **identified** by 4 tuple: source IP address, source Port number, destination IP address, destination Port number
- **TCP connection establishment**:
    - **Step 1**: Server process must at first be running, create socket that welcomes client’s contact
    - **Step 2**: Client must contact server in Step 1 by creating TCP socket, _specifying_ IP and port # of server host process
    - **Step 3**: After Step 2 is done, server that’s contacted by client must create a new socket for server process to communicate with that particular client
    - **Step 4**: After Step 3 is done, server process can continue accepting more clients, while communicating with multiple clients (with each different socket) who have established prior TCP connections using the same step (b) and (c)

**Demultiplexing**: receiver uses all four values to direct segment to the appropriate TCP socket. 
**Multiplexing**: server host support many simultaneous TCP connection, each socket is identified by its own unique 4-tuple.

The diagram below illustrates how demultiplexing and multiplexing is done:

![[Transmission Control Protocol (TCP)-1.png]]

# Three-Way Handshake
![[Transmission Control Protocol (TCP)-2.png]]

The TCP three-way handshake is a crucial process used to establish a reliable connection between a client and a server in a TCP/IP network. This process ensures that both parties are **ready** to **transmit** and **receive** data.

1. `SYN` (Synchronize)

- **Initiator**: Client
- **Description**: The client initiates the connection by sending a TCP segment with the SYN flag set. This packet includes an initial sequence number (ISN), which is a random value chosen by the client.
- **Purpose**: To inform the server that the client wants to establish a connection and to synchronize sequence numbers.
- **Steps**:
	- The client sends a SYN packet to the server to initiate a connection.
	- The packet contains the client’s initial sequence number (ISN = X).

```
Client -> Server: SYN, Seq = X
```

2. `SYN-ACK` (Synchronize-Acknowledge)

- **Initiator**: Server
- **Description**: Upon receiving the SYN packet from the client, the server responds with a TCP segment that has both the SYN and ACK flags set. The server’s packet includes its own initial sequence number and acknowledges the client’s sequence number by incrementing it by one.
- **Purpose**: To acknowledge the client’s SYN packet and provide the server’s initial sequence number.
- **Steps:**
	- The server responds with a SYN-ACK packet, acknowledging the receipt of the client’s SYN packet.
	- The packet contains the server’s initial sequence number (ISN = Y) and acknowledges the client’s sequence number by setting the acknowledgment number to X+1.

```
Server -> Client: SYN, ACK, Seq = Y, Ack = X + 1
```

3. `ACK` (Acknowledge)

- **Initiator**: Client
- **Description**: The client sends a final TCP segment with the ACK flag set. This packet acknowledges the server’s SYN-ACK packet by incrementing the server’s sequence number by one.
- **Purpose**: To acknowledge the server’s SYN-ACK packet and finalize the connection establishment.
- **Steps:**
	- The client sends an ACK packet to the server, acknowledging the receipt of the server’s SYN-ACK packet.
	- The packet contains the client’s next sequence number (X+1) and acknowledges the server’s sequence number by setting the acknowledgment number to Y+1.
	- **Piggybacking**: data can be sent along with an acknowledgment in the same packet.
	    - However, The final ACK in the TCP handshake acknowledges the server’s SYN-ACK and doesn’t need to carry any data.
	    - While the client may piggyback data with the ACK if ready, it’s not required; the ACK can simply be an empty acknowledgment in TCP.

```
Client -> Server: ACK, Seq = X + 1, Ack = Y + 1
```


**Visualization of the Three-Way Handshake**

```
Client                    Server
  |       SYN, Seq=X       |
  |----------------------->|
  |       SYN, ACK         |
  |      Seq=Y, Ack=X+1    |
  |<-----------------------|
  |       ACK, Seq=X+1     |
  |       Ack=Y+1          |
  |----------------------->|
```

Summary:
In short, the **SYN** packet is used to initiate the connection. The **SYN-ACK** packet is used to acknowledge the SYN packet and provide the server’s sequence number. Finally, the **ACK** packet is used to acknowledge the SYN-ACK packet and finalize the connection establishment.

>[!Note]
>The three-way handshake is essential for establishing a reliable TCP connection, ensuring that **both** the client and server are ready to communicate and have synchronized sequence numbers for the data transfer that follows. You will be able to see the SYN, SYN-ACK, and ACK packets in the later labs using packet sniffing tools like Wireshark.

