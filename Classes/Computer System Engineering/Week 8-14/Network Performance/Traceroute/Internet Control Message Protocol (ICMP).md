---
aliases:
  - ICMP
---

It is a [[Protocols|protocol]] for error messages and operational information (standard messages), mainly not used by the [[Application (User) Program|application]] itself but used by the network operators to identify errors, perform diagnostics, and generally are used for control purposes.

ICMP is actually implemented at the “**top**” of [[5 Layer OSI Model#Network Layer|layer 3 (network layer)]]. It relies on IP protocol to deliver data to a remote host. In other words, ICMP messages must be encapsulated in IP [[Packets]].