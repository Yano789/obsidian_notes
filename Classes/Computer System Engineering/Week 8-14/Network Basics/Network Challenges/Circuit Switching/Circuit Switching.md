A type of network **configuration** where we reserve all resources (physical path) required to provide for communication between two [[End Systems]] for the duration of their designated communication session (not forever).

![[Circuit Switching - 1.webp]]
*In the figure above, there are three resources (routers / switches) that’s required for host A and B to communicate. For as long as A and B are communicating, the three resources: R1, R2, and R3 are reserved for them.* 

**Pros:** The **advantage** of circuit switching is that we have a guaranteed stable connection for that reserved slot / bandwidth.

**Cons:** The **drawback** of circuit switching is that user $j$ cannot utilize the resources that user j has in the other time slot or frequency band. It is possible for a user to underutilize its resources, not to mention that it is *expensive*.

# Multiplexing the Circuit
If there’s other hosts that would like to communicate using these resources R1, R2, and R3, host A and B must somehow share this resource, albeit being reserved. We can do this using either of the two methods:

- [[Frequency Division Multiplexing (FDM)]]: each circuit continuously gets a fraction of the bandwidth (e.g: 4KHz as shown), or
- [[Time Division Multiplexing (TDM)]]: each circuit gets all of the link bandwidth periodically during brief intervals of time slots.

>[!IMPORTANT]
>For example calculations, visit
>https://natalieagus.github.io/50005/ns/01-network-basics#internet-protocols-and-apis

