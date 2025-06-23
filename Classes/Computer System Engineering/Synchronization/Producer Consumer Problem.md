Two [[Process#Asynchronous Processing|Asynchronous Processes]] or [[Threads]] are trying to write to and read from the same bounded buffer [[Process#Concurrency|concurrently]] 

# Precedence Constraints
- Producer cannot produce too much before consumer consumes
- Consumer cannot consume before producer produces

 >[!WARNING] Without proper synchronization attempts, the precedence condition will be violated

This is due to the presence of the [[Race Condition]] 

