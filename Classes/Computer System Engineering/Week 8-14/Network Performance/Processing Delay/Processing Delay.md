the time it takes for a **network device**, such as a router or switch, to examine a packet’s **header** and determine where to forward the packet. (pretty self explanatory)

![[Processing Delay - 1.webp]]

**Duration**: < milliseconds, usually is bounded or fixed. It is affected by the device’s performance (e.g: router’s CPU speed, memory speed, and its software efficiency).

**Cause**: Needs time to examine packet header.
- Check for bit errors (checksum),
- Compute output link as denoted by destination IP address.