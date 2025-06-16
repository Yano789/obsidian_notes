
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

# Armstrongs Axioms
## Reflexivity
$$
Y \subseteq X \Rightarrow X \rightarrow Y, \ X \subseteq Z \Rightarrow XZ \rightarrow X
$$

## Augmentation
$$
X \rightarrow Y \Rightarrow XZ \rightarrow YZ
$$

## Transitivity
$$
X \rightarrow Y \land Y \rightarrow Z  \Rightarrow X \rightarrow Z
$$

