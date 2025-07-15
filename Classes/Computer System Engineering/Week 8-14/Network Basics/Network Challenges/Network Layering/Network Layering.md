Network layering is a **design principle** in computer networking where each layer of a network architecture performs specific functions and only interacts with the layers directly above and below it.

When discussing the “modules” in the Internet, it could refer to various hardware and software components that are necessary for the Internet to function.

These include:
- Routers and switches, which direct data traffic.
- Servers, which store and deliver content such as websites.
- Transmission media, such as cables and wireless signals that carry the data.
- Protocols, such as TCP/IP, which define the rules for transmitting data.

In programming, we try to tackle complicated systems all the time by making our code more **modular**. However, modularity is not the answer to organize the internet architecture because:
- Modules can interact with every other modules, that means we need to consider N2
- possible interactions between N modules.
- Due to point (1), you may result in emergent behaviour:
    - Erroneous behaviours that aren’t observed in the modules individually, but arise when you let one module interact with another (you suffer from this a lot from 50.002 1D project).
    - Example: **priority inversion** caused by priority scheduling + locking mechanism (recall the OS topics). This caused something important (of a higher priority) to inadvertently become the lowest priority due to some misguided usage of **locking** mechanism. _Head to class activity to find out more_.

Example of Network Layering: 
- [[5 Layer OSI Model]]
- [[Software-Defined Networking (SDN)]] 