a *software-based* approach to solve The [[Critical Section (CS)]] Problem with 2 restrictions
1. Two [[Process|processes]] that **alternate** execution between their [[Critical Section (CS)]] and remainder sections

>[!NOTE] 
>Single core environment only

2. Architectures where `LD` and `ST` are [[Atomic Operation]]
# Key Idea
This solution works by initializing two global variables
```C
int turn;
bool flag[2];
```

In the case of 2 [[Process|processes]] ($P_i \ \text{and} \ P_j$)
- if `turn == i`, process `Pi` is allowed to enter the [[Critical Section (CS)]]. Otherwise,
- If `flag[i] == true`, process `Pi` is ready to enter the [[Critical Section (CS)]]

Uses [[Spinlock|busy waiting]] 
# Algorithms
```C
// FOR Pi
do{
	flag[i] = true;
	turn = j;
	while(flag[j] && turn == j); // WAIT HERE FOR ACCESS
	// CRITICAL SECTION HERE
	// ...
	flag[i] = false;
	// REMAINDER SECTION HERE
	// ...
}while(true)
```

> [!NOTE] 
> Similarly, the code for process $P_j$ is just the same with flipped letters


