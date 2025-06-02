Divided into four components:
1. Hardware
	1. CPU 
	2. I/O [[Device Controllers]] 
2. [[Operating System (OS)]]
3. Application/[[Application (User) Program]]
4. Users

![[The-Computer-System-1.webp]]

## System Structure
### Multiprocessor System
Main advantages:
- **Increased throughput**: executing many processes in parallel
- **Economy of Scale**: cheaper than multiple single processor system
- **Increased Reliability**: If one core fails, we still have other cores to do the work 

#### Symmetric Architechture
![[The Computer System-1.webp]]

*Notice how we have multiple CPU's*

#### Multi-Core Architechture
![[The Computer System-2.webp]]

*On-chip communication is faster than across chip communication*

#### Asymmetric Multiprocessing
Each processor is assigned a specific task with the presence of a super processor that control the system
- **master-slave** relationship

### Clustered System
are multiple systems that work together

1. Share storage via network
2. High availability service
3. High Performance Computing

**Two types of Clustering**
1. Asymmetric Clustering - one machine in hot-standby mode
2. Symmetric Clustering - multiple machines keeping each other in check