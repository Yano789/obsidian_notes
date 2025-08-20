measures the delay from the source to each router along the internet path towards a destination.

![[Traceroute - 1.webp]]

Traceroute is a network diagnostic tool used to trace the path that data [[Packets]] take from one point to another on a network. Traceroute relies on [[Internet Control Message Protocol (ICMP)]] ([[Network Layering|Network Layer Protocol]]) to work.

It works by sending a series of [[Packets]], each forming a **probe** with an incrementally increasing **time-to-live** (TTL) value, towards the destination. The TTL value determines how many network hops (routers) the packet can pass through before being discarded. 
1. Each router decrements the TTL value by one. 
2. When the TTL reaches zero, the router discards the packet and sends an **ICMP Time Exceeded** message back to the sender.

# Probe
At each probe $i$, traceroute sends 3 [[Packets]] that will reach router $i$ (means the router reached after $i$ hops) on path towards destination. These packets are **ICMP Echo Packets** with TTL (time to live) value of $i$. Each router in the path will decrease the TTL by 1.

The final value of $i$ is unknown in the beginning. 
- It starts from 1 and it will be increased by 1 at each iteration. 
- It’s maximum is set to be certain number, e.g: 64.

Router at hop $i$ will be the last router in the path that decreases the TTL (TTL will reach 0 at this point), and will respond to the sender, the `traceroute` process, by sending **"ICMP TTL Exceeded Packet"** because it is not the destination router.

# Round Trip Time (RTT)
The traceroute process measures the time from packet sent until packet is received back from router $i$ for each probe. RTT depends on various factors: 
1. network infrastructure, 
2. distance between nodes, 
3. network conditions, and 
4. packet size.

Traceroute listens for these ICMP messages, recording the IP addresses of the routers along the path. By repeatedly sending packets with increasing TTL values and recording the responding routers, traceroute builds a map of the network path to the destination.

# Termination
The traceroute program (in UNIX-like OS) sends [[Packets]] to a likely unusable port in the destination, e.g: 50000. When the packet reaches the destination, the destination host finds out that the packet is destined for a port that is unusable.

The destination host will send back an **ICMP Port Unreachable Message**, where upon receiving this the traceroute program stops sending more [[Packets]].

