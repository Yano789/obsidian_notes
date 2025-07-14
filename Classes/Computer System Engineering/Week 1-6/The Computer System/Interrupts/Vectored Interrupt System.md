an [[Interrupt]] signal that **INCLUDES** the *identity of the device* sending the signal
- this allows the [[Classes/Computer System Engineering/Week 1-6/The Computer System/Operating System (OS)/Kernel/Kernel|Kernel]] to know exactly which [[Interrupt]] service routine to execute
- **complex to implement** but useful when the system throws many [[Interrupt|interrupts]] 

This system accepts an **ADDRESS**, which is usually one of a small set of numbers for an offset into a table called the [[Interrupt Vector]]

Each [[Interrupt]] source is associaed with a unique **vector address** which allows direct access to the appropriate interrupt handler
