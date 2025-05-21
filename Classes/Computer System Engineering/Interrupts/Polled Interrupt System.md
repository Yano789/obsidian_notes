The interrupted program enters a general **interrupt polling routine protocol** (single entry point), where the CPU scans (*polls*) devices to determine which device made the **service request**

No interrupt signal that includes the identity of the device sending the signal

The [[Classes/Computer System Engineering/The Computer System/Operating System (OS)/Kernel|Kernel]] must send a signal out to each [[Device Controllers]] and read the interrupt status register or other means

*Note: This is easier to implement but more time-consuming to run*


