defined as a **segment** of a [[Process]] (has at least one thread)

A process can have **multiple** threads, and we can define thread as a basic unit of CPU utilization; it comprises of:

- A **thread ID**,
- A **program counter**,
- A **register** set, and
- A **stack**.

![[Pasted image 20250614165659.webp]]

# Multithreading Benefits
1. Responsiveness
2. Easy Resource Sharing and Communication
3. Threads are Lighter
	1. cheaper for one [[Process]] to share resources than to create new [[Process|processes]] 
	2. Note: [[Context Switching]] is pure [[Overhead]]

# Types of Threads
## 1. User Level Threads
- scheduled by a **runtime library** or virtual environment
- managed in the user space
- what programmers typically use

## 2. Kernel Level Threads
- an execution unit within the [[Classes/Computer System Engineering/Week 1-6/The Computer System/Operating System (OS)/Kernel/Kernel|Kernel]] to perform tasks on behalf of the [[Classes/Computer System Engineering/Week 1-6/The Computer System/Operating System (OS)/Kernel/Kernel|Kernel]] 