
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
![[Relational Algebra-1.png|371x140]]

___
## Product ($\times$)
- Matrix Multiplication
$$
(R \times S)
$$
```SQL
select * from R cross join S;
```

Example:
![[Relational Algebra-2.png|323x399]]

___
## Join ($\bowtie$)
### Inner Join
- Return tuples in $R\times S$ and satisfying a condition
$$
(R \bowtie_{R.A = S.D}S)
$$

Example:
```SQL
select * from R, S
where R.A = S.D;
```
![[Relational Algebra-3.png|345x327]]

___
### Natural Join
- Inner join but:
	- detect attributes with same names
	- remove duplicates
$$
(R \bowtie S)
$$
Example:
```SQL
select * from R natural join S;
```

![[Relational Algebra-4.png|342x382]]

___
### Left Outer Join
- Same as inner join but:
	- all tuples of R appear in the result
![[Relational Algebra-5.png|174x45]]

Example:
```SQL
select * from R 
left outer join S on R.A = S.D;
```

![[Relational Algebra-6.png|336x358]]

___
### Rename
$$
\rho_{R'}
$$