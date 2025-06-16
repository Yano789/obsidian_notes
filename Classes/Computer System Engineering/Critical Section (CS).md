A predefined section of the [[Program]] that can guarantee and [[Atomic Operations|atomic operation]] is called the **Critical Section (CS)**

> [!IMPORTANT] 
> When one [[Process]] is executing its critical section, no other [[Process]] is allowed to execute its critical section 

> [!WARNING] 
> It is a challenging problem to protect a critical section. This is because it will take time and resources ([[Overhead]]) to make sure other [[Process|processes]] do not run at the same time. 

___
# Requirements for CS Solution
## Mutual Exclusion (MutEx)
- Don't let a [[Process]] in the critical section if there is already one there

## Progress
- Grant access to the critical section if there is no [[Process]] in the critical section

## Bounded Waiting
- If a [[Process]] keeps entering the critical section, it will eventually have to give way for another [[Process]] to enter

> [!TIP]
> Mutual Exclusion and Progress are the most important for this section

___
# Properties for CS Solution
## Safety
- there should be no [[Race Condition]]

## Liveness
- a [[Program]] with a proper CS solution will not hang forever

___
# Solution Template
```C
while(true){
	[ENTRY SECTION]
		CRITICAL SECTION ...
		...
	[EXIT SECTION]
		REMAINDER SECTION ...
		...
}
```

The protocol causes a [[Process]] to:
1. **REQUEST** for permission to enter (ENTRY SECTION)
2. **EXECUTE** the critical section when request is granted
3. **EXIT** the CS solution
	1. There may exit a remainder section that continues on after the exit section

> [!NOTE]
> The rest of the [[Program]] that is not in the critical section is called the **remainder section**

