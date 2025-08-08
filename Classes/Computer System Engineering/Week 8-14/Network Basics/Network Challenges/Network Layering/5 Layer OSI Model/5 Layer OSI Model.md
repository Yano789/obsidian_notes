![[5 Layer OSI Model-1.png]]

# Application Layer
This is implemented as software, typically the user application(s) needing to communicate via the internet itself. This layer is where network **applications** and their application-layer protocols reside: the layer that provides [[Application Programming Interface|API's]] for web-applications to rely on.

Examples of [[Protocols]] in the Application Layer and their associated libraries/frameworks:
1. **HTTP** (Hypertext Transfer Protocol): used for transmitting hypertext documents on the World Wide Web.
    - Libraries/Frameworks: Express.js (Node.js), Flask (Python), Spring Boot (Java), Django (Python), Ruby on Rails (Ruby), ASP.NET (C#), etc.
2. **SMTP** (Simple Mail Transfer Protocol): used for sending email messages between servers.
    - Libraries/Frameworks: JavaMail (Java), Flask-Mail (Python), Nodemailer (Node.js), Spring Mail (Java), etc.
3. **FTP** (File Transfer Protocol): used for transferring files between a client and a server on a computer network.
    - Libraries/Frameworks: Apache Commons Net (Java), ftplib (Python), Net::FTP (Perl), libcurl (C/C++), etc.
4. **DNS** (Domain Name System): used for translating domain names into IP addresses and vice versa.
    - Libraries/Frameworks: dnsjava (Java), dnspython (Python), Net::DNS (Perl), etc.
5. **SSH** (Secure Shell): used for secure remote access and secure file transfer over an insecure network.
    - Libraries/Frameworks: JSch (Java), Paramiko (Python), Net::SSH (Perl), etc.
6. **[[Socket]] / WebSocket**: provides full-duplex communication channels over a single TCP connection.
    - Libraries/Frameworks: ws (Node.js), websocket-client (Python), WebSocket API (JavaScript), etc.

>[!NOTE]
>An application layer packet of information is called a **message**.

# Transport Layer
This is also implemented as software. This layer must reliably assist to transport application-layer messages between application endpoints.

>[!NOTE]
>Transport layer [[Protocols]] are typically implemented as part of the operating system’s networking stack.

Two of the most common transport layer protocols are:

1. [[Transmission Control Protocol (TCP)]]
2. [[User Datagram Protocol (UDP)]]

Application layer protocols **rely** on transport layer protocols. For instance, HTTP relies heavily on [[Transmission Control Protocol (TCP)]] for reliable and ordered delivery of web page data. On the other hand, DNS primarily uses [[User Datagram Protocol (UDP)]] because DNS queries are typically short and require quick responses. You will learn more about these protocols specifically in the later weeks.

>[!NOTE] 
>A transport layer packet of information is called a **segment**

## Packet Header Format

Information from the **packet header** will be used to demultiplex incoming packets to the correct socket, depending on whether the socket is UDP or TCP:

![](https://natalieagus.github.io/50005//docs/NS/images/08-app-layer/2024-05-09-12-28-38.png)

Note that this is a very simplified illustration. In practice, the packet header has all sorts of information, like source and destination port, source IP and destination IP, but **not all** may be used to identify sockets in the destination host, depending on whether the Socket in question relies on TCP or UDP.

Further information like IP addresses, MAC addresses, network topology information, and port number are typically accessible even at application layer even though application layer protocols dont directly manage these stuffs. These further information is made available for several reasons like diagnostics and logging, access control, security, session management, and many more.

## Multiplexing and Demultiplexing
Since there are **many** applications that can be running on the hosts, the transport layer protocol multiplex at sender and demultiplex at receiver:

- **Multiplexing**: Multiplexing at the transport layer involves **combining** data from multiple application processes into a **single stream** of packets that can be sent over the network. The transport layer adds necessary **headers** (including source and destination port numbers) to each packet before passing them to the network layer.
- **Demultiplexing**: Demultiplexing is the process by which the transport layer **receives** packets from the network layer and **directs** them to the appropriate application process. This involves examining the headers of incoming packets to determine which application process should receive the data.

![[5 Layer OSI Model.png]]

>[!Note]
>In the context of TCP and UDP, multiplexing and demultiplexing are handled by the **kernel’s transport layer**. The kernel uses port numbers in the transport layer headers to route incoming packets to the correct application process and to send outgoing data from multiple processes over the network efficiently.

When a TCP segment arrives, the kernel uses the **destination** **port** number, along with the **source** **IP**, **source** **port**, and **destination** **IP**, to identify the socket that is managing the connection. The segment is then passed to the appropriate socket buffer for the corresponding application process to read.

When a UDP datagram arrives, the kernel uses the **destination** **port** number + destination (this host’s) IP number to find the UDP socket _bound_ to that number. It does not utilise source IP and source port to identify the UDP socket since UDP socket is _connectionless_.

# Network Layer
The network layer can consist of both software and hardware components. Devices or softwares in this layer is responsible for routing datagrams through a series of routers between the source and destination (i.e: it does path planning).

Below are some examples:
1. **Network Layer Protocols**: Primarily implemented in **software**
    - **IP**: Routes and addresses packets across networks in the Internet Protocol Suite.
    - **ICMP**: Provides diagnostics and error reporting within IP networks.
    - **OSPF**: Determines optimal routing paths within autonomous systems.
    - **BGP**: Facilitates routing between autonomous systems on the Internet.
2. **Network Layer Devices** (e.g: these are devices made solely to support _up to_ network layer):
    - **Router**: Forwards data packets between computer networks based on IP addresses.
    - **Layer 3 Switch**: Combines switching and routing functions at wire speed.
    - **Network Firewall**: Filters and controls network traffic based on predefined security rules.
    - **Gateway**: Acts as an entry or exit point between different networks, translating protocols or addressing schemes.
3. Software (implementation):
    - **Routing Protocol Software** such as Quagga, an open-source routing software suite that supports various routing protocols and is commonly used on Linux-based routers.

**Difference with transport layer protocols:** the Internet transport-layer protocols ([[Transmission Control Protocol (TCP)]] or [[User Datagram Protocol (UDP)]]) in a source host passes a transport-layer **segment** and a destination address to the network layer, just as you would give the postal service a letter with a destination address. The network layer then provides the service of actually delivering the **segment** (now called datagram) to the transport layer in the destination host.

>[!NOTE]
>A network layer packet of information is called a **datagram**.

# Link Layer
Most Link Layer utilities are implemented in hardware, such as bit error detection, with its software part implements the higher level functionality and activates the controlling hardware.

Its job is to provide reliable delivery service of packets from one node to another in the (already known) route. Link layer devices or software does not route, it simply delivers the [[Packets]] of information to the next node which is already determined by the network-layer.

Below are some examples:
1. **[[Protocols]]**: Primarily implemented as combination of both **hardware** and **software**
    - **Ethernet**: Manages communication over local area networks (LANs) using MAC addresses.
    - **ARP** (Address Resolution Protocol): Maps IP addresses to MAC addresses for data transmission within a network.
    - **PPP** (Point-to-Point Protocol): Establishes direct connections between two nodes over a serial link.
2. **[[Device Controllers|Devices]]**:
    - **Ethernet Switch**: Forwards data frames between devices within a LAN based on MAC addresses.
    - **NIC** (Network Interface Card): Connects a computer or device to a network, handling data transmission at the link layer.
    - **Wireless Access Point** (WAP): Connects wireless devices to a wired network, managing wireless communication at the link layer.
    - **Ethernet Hub** (deprecated): Shares network bandwidth among connected devices by broadcasting data frames to all ports.
3. **Software**:
    - **NIC Driver**: Implement link layer protocols such as Ethernet and provide an interface for the operating system to send and receive data frames over the network.

To move [[Packets]] from one node (host or router) to the next node in the route, the network layer relies on the services of the link layer. In particular, at each node, the network layer passes the **datagram** down to the link layer, which delivers the **datagram** (now called frame) to the next node along the route.

>[!NOTE]
>A link layer packet of information is called a **frame**.

# Physical Layer
This is implemented purely as **hardware**.

The job of the link layer is to move entire frames from one network element to an adjacent network element, while the job of the physical layer is to move the individual bits within the frame from one node to the next.

[[Protocols]] on this layer depend on the medium of transmission: twisted pair copper wire, optical fibre, etc.

Below are some examples:
1. **[[Protocols]]**:
    - **Ethernet Physical Layer**: Defines the physical characteristics and transmission medium for Ethernet networks, including cable types and signaling methods.
    - **IEEE 802.11 (Wi-Fi)**: Specifies the physical layer for wireless local area networks (WLANs), including modulation techniques and frequency bands.
2. **[[Device Controllers|Devices]]**:
    - **Ethernet Cable**: Transmits electrical signals between devices in an Ethernet network, such as twisted pair cables (e.g., Cat5e, Cat6).
    - **Wireless Antenna**: Sends and receives radio signals to communicate with wireless devices in Wi-Fi networks.
    - **Ethernet Transceiver**: Converts digital data into signals suitable for transmission over Ethernet cables, and vice versa.
    - **Fiber Optic Cable**: Transmits data using light signals through glass or plastic fibers, providing high-speed, long-distance communication in fiber optic networks.

>[!NOTE]
>A physical layer packet of information is called a frame.

