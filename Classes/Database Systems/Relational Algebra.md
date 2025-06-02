
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

