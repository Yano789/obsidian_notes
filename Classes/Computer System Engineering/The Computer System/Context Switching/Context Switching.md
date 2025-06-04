---
aliases:
  - Context Switch
---

Context switch is the routine of **saving** the state of a process in its corresponding [[Process#Process Control Block (PCB)]], so that it can be **restored** and **resumed** at a later point in time.

Benefits:
- [[Timesharing]] - **Rapid Context Switching**: when the [[Process]] is suspended, it's context gets stored in the [[Process#Process Control Block (PCB)]] 

Drawbacks:
- [[Overhead]]

![[Context Switch-1.webp|377x328]]

