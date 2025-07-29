refers to the **efficiency** and **reliability** of data transmission across a network.

There are **4 sources of packet delays** that affect network performance
![[Network Performance - 1.webp]]

1. [[Processing Delay]]
2. [[Queueing Delay]]
3. [[Transmission Delay]]
4. [[Propagation Delay]]

**Total Nodal Delay**
The total nodal delay (from one node/router) to another node/router is the sum of all types of delays: 
$$
d_{nodal}=d_{proc}+d_{queue}+d_{trans}+d_{prop}
$$

**Average Link Utilization**
The average link utilization model is obtained from observation. The model below is assumed based on random and bursty [[Packets]] arrivals:

![[Network Performance - 2.webp]]

The average queueing delay is related to the average link utilization (traffic intensity). It approaches infinity as the average link utilization approaches 1.

The formula for average link utilization is:
$$
\frac{La}R
$$
where 
- L is packet length in bits, 
- a is average packet arrival rate (packets/second), and 
- R is the link’s bandwidth in bits

>[!IMPORTANT]
>Queueing delay is a convex increasing function of utilization:
>- **If average link utilization 0**, average queueing delay is small
>- **If average link utilization is near 1**, average queueing delay is large
>- **If average link utilization > 1**, average queueing delay is infinite (there’s more work arriving that can be serviced)

# Throughput and Bandwidth
**Throughput** (RATE) is defined as the rate (bits/time unit) at which bits are actually transferred between sender/receiver. 
**Bandwidth** (MAXIMUM) is defined as the maximum amount of data that can travel through a link.

Throughput computation is application specific, depending on factors such as latency, SNR (hardware limitations), etc. For example, at [[Transmission Control Protocol (TCP)]] level, the throughput depends on [[Traceroute#Round Trip Time]] and window size.

Throughput is different from bandwidth. Bandwidth is the theoretical maximum capacity of a network link, while throughput is the actual observed data transfer rate under real-world conditions.

There are **two** ways to calculate throughput:
- **Instantaneous** throughput: if the measurement is taken over a very short time interval
- **Average** throughput: if the measurement is taken over a long time interval, for example, the transfer a bunch of large files.

Average throughput is usually more consistent than instantaneous throughput. Average throughput represents the data transfer rate over a longer period, smoothing out fluctuations and providing a more stable indication of network performance compared to instantaneous throughput, which may vary significantly due to factors like congestion, bursty traffic, or network conditions.

Link bandwidth varies depending on its material/technology:

- T1 Line (1.5 Mbps)
- Fast Ethernet (100 Mb/s)
- T3 Line (43 Mbps)
- Gigabit Ethernet (1Gb/s)
- OC192 (9.95 Gb/s)

This capacity of a link (bandwidth) is a **combination** of the physical characteristics of the transmission medium, the technology and standards applied, the quality and configuration of the network equipment, and the environmental conditions in which the network operates. You will learn more about it if you take a full Networks class, but you can read this [appendix](https://natalieagus.github.io/50005/ns/03-network-performance#factors-affecting-bandwidth) section if you’re curious about what factors affect bandwidth.

We can compute end-to-end throughput based on the bottleneck link. For instance, given the following network topology and bandwidth:
![[Network Performance.png]]
If Host A wish to send packets to host C, where the _throughput_ of each link is as shown in the diagram above, Host A can only do so with throughput of 3 MBps.

>[!NOTE]
>It’s common to use the term “bandwidth” when discussing network topology and link capacities in throughput computation questions. This is because in **theoretical** or **simplified** network scenarios, the bandwidth of a link represents its maximum capacity, which is a key factor in determining the _potential throughput_ of data transmission across that link. 
>
>Therefore, while “throughput” refers to the actual observed data transfer rate, in theoretical scenarios or when designing networks, it’s often assumed that the link operates at its maximum capacity (bandwidth) under ideal conditions. Therefore, using “bandwidth” in such contexts is appropriate for simplicity and clarity in calculations and network design discussions.

# Visualization
## Space Time Diagram
- **Vertical** = **time**, while **horizontal** = **space** between source and destination points (distance). You can compute the last bit transmitted given **$L$ (packet length)** and **$R$ (bandwidth)**.
- Here we often **omit the illustration of queueing delay**
- We also **omit the illustration of transmission delay for negligible-sized packets** (e.g: packets so small that transmission delay won’t matter)
- We also **severely simplify the diagram** and assume that there are no other nodes between the source and destination (this is not true in practice, as the packets between source and destination would need to go through several routers)

![[Network Performance-1.png]]