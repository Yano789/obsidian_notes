
$$
X_1 \ ... \ X_m \rightarrow Y_1 \ ... \ Y_m
$$
$$
\text{Left Hand Side (LHS)} \rightarrow \text{Right Hand Side}
$$
$$
X \ \text{determines} \ Y
$$
Check if:
 1. FD is violated in the table
 2. Even if FD is not in the [[Relational Model#Instance]] doesn't mean it's not in the [[Relational Model#Schema]]
$$
\text{If} \ X \rightarrow Y, \text{and} \ X\rightarrow Z, \text{then} \ X \rightarrow YZ
$$
>[!WARNING]
>$XY\rightarrow Z \neq X \rightarrow Z, Y \rightarrow Z$
___

# Solving FD Problems
1. Compute [[Closure Set]]($F^+$) w.r.t. one of the attributes
	1. eg. $A \rightarrow BC \Rightarrow C\rightarrow E$
	2. $A\rightarrow B \ A \rightarrow C \Rightarrow A \rightarrow E$
	3. Therefore $A\rightarrow \{A,B,C,E\}$  
	4. Since it is missing D, our candidate key becomes $AD \rightarrow \{A,B,C,D,E\}$

>[!NOTE] If only 1 attribute is your candidate key, it will definitely be 2NF because there will be no partial dependency
