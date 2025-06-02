---
tags:
  - review
---

## Data Definition

### Create Database and Tables
```SQL
create database if not exists university;

create table Payroll (
	UserID integer,
	Name varchar(100),
	Job varcher(100),
	Salary integer
	primary key (UserID, Car) //use only if you need a primary key! (if no primary key, there may be duplicates when addint)
	foreign key (UserID) references Payroll(UserID) //references current table key with another table "payroll"
);
```

*Case insensitive (except for Table name)*


## Data Manipulation
### Add New Data into the Table
```SQL
insert into Payroll values (001, "Kenny", "Prof", 10000);
insert into Payroll values (002, "Fiona", "TA", 10000);

insert into Payroll values (001, "Kenny", "Prof", 10000),
							(002, "Fiona", "TA", 10000); //same thing except shorter
```

[[Relational Model]] uses **set semantics** (no duplicates)
[[SQL]] uses **bag semantics** (can have duplicates)

### Extract, Transform, Load (ETL)

```SQL
load data infile "payroll.csv" into table Payroll
fields terminated by ',' Enclosed by '"'
lines terminated by '\n'
ignore 1 rows;
```

*Note: search ETL for your DBMS because it is different for all*

## Query

```SQL
SELECT Col1, Col2, ... //Projection / Rename / Columns
FROM R1, R2, ... //Product / Tables
WHERE Conditions //Selection / sigma (σ)
```

```SQl
select * from Payroll // * represents all
where Salary > 70000; // Condition

select UserID, Salary from Payroll // specific attributes
where Salary > 70000; // Condition / sigma (σ)
```

### Searching in SQL
```SQl
select p.Name, r.Car
from Payroll p, Registr r
where p.UserID = r.UserID // Join Condition
```

```SQl
select p.Name, r.Car
from Payroll p left outer join Registr r // Joining based on the first column of Payroll
on p.UserID = r.UserID
```

```SQl
select p.Name, r1.Car as 'car1', r2.Car as 'car2'
from Payroll p, Registr r1, Regist r2
where p.UserID = r1.UserID
and r1.UserID = r2.UserID
and r1.Car = "Civic" and r2.Car = "Pinto"
```

### Distinct

```SQL
select distinct Job from Payroll;

select distinct Name, Job from Payroll;
```

### Aggregates

1. AVG
2. MIN
3. MAX
4. SUM
5. COUNT

```SQL

```

### Group By
- **USEFUL**
- Project tuples into *distinct groups*, then compute aggregate
- You cannot double group by because the 1st group by isnt finished processing yet
```SQL
select Job, avg(Salary) as 'AvgPerJob'
from Payroll group by Job;
```

### Having
- selects the output from **GROUP BY**
```SQL
select Job, avg(Salary) as 'AvgPerJob'
from Payroll group by Job
HAVING AvgPerJob > 60000;
```

### Limit
- Restrict the number of output tuples

### Order By
- sort the tuples 
```SQL
select Name, Salary from Payroll
order by Salary desc;
```

## Nested Queries
