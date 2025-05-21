the process of starting up a computer (usually *hardware initiated*)

## Bootstrapping
Initially loads the **Firmware (BIOS)**, and eventually the [[Operating System (OS)]] to the main memory to be executed by the CPU

![[Classes/Computer System Engineering/The Computer System/Operating System (OS)/Booting/Blue Skies and Sunshine-1.webp]]

1. Prepare Ready-to-go devices to be used by the [[Operating System (OS)]] 
2. Loads other programs, which will load more complex programs
3. Loads the [[Classes/Computer System Engineering/The Computer System/Operating System (OS)/Kernel|Kernel]] from the disk
4. Initialize in *kernel mode*, after setting up everything the [[Operating System (OS)]] is loaded and switched to *user mode*  

## The Booting Paradox
Load a *special program* onto the main memory from a **Read-Only-Memory (ROM)** that comes with the motherboard. This is called the **Firmware (BIOS)** 