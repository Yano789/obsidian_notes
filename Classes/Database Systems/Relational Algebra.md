
| Symbol    | Function     |
| --------- | ------------ |
| $\sigma$  | Selection    |
| $\pi$     | Projection   |
| $-$       | Difference   |
| $\cup$    | Union        |
| $\cap$    | Intersection |
| $\bowtie$ | Join         |
| $\times$  | Product      |
| $\rho$    | Rename       |
| $\gamma$  | Aggregation  |
___
## Selection ($\sigma$)
- Acts as a filter
- You can use conjunction (AND)  and disjunction (OR)
- Corresponds to [[SQL#Query|WHERE in SQL]]
$$
\sigma_{\text{predicate}(R)}
$$
Example:
$\sigma_{A='a2' \text{AND} B>102}(R)$ 
```SQL
select * from R
where A = 'a2' and B > 102;
```

___
## Projection $\pi$
- Return tuples with specific attributes
- Corresponds to [[SQL#Query|SELECT in SQL]]
$$
\pi_{A1,A2...}(R)
$$

Example:
$\pi_{B-100, A}(\sigma_{A='a2'}(R))$
```SQL
select B-100, A from R
where A = 'a2';
```

___
## Union ($\cup$)
- Return Tuples appearing in any of the two relations
	- No Duplicates
$$
(R \cup S)
$$

Example:
$R \cup S$
```SQL
(select * from R) UNION (select * from S);
```

___
## Intersection ($\cap$)
- Return Tuples appearing in both relations
$$
(R \cap S)
$$

Example:
$R \cap S$
```SQL
(select * from R) INTERSECT (select * from S);
```

___
## Difference ($-$)
- Return tuples appearing in R but not S
$$
(R-S)
$$
Example:
R(A,B)

| A   | B   |
| --- | --- |
| a1  | 101 |
| a3  | 102 |

S(A,B)

| A   | B   |
| --- | --- |
| a3  | 102 |
| a4  | 104 |

R - S

| A   | B   |
| --- | --- |
| a1  | 101 |

___
## Product ($\times$)
- Matrix Multiplication
$$
(R \times S)
$$
