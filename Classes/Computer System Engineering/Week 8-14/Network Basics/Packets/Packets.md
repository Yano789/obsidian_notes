---
aliases:
  - packet
---
When one end system has data to send to another end system, the sending [[End Systems|end system]]:

- **Segments** the data (into smaller chunks) and
- Adds **header bytes** to each segment (to know the order of the chunks)

The resulting packages of information, known as **packets** in the jargon of computer networks, are then sent through the network to the destination end system, where they are **reassembled** into the original data. *This means they follow encapsulation* 

![[Packets - 1.png]]