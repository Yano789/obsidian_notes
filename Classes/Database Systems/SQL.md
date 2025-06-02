## Data Definition

### Create Database and Tables
```SQL
create database if not exists university;

create table Payroll (
	UserID integer,
	Name varchar(100),
	Job varcher(100),
	Salary integer
	primary key(UserID, Car) //use only if you need a primary key!
);
```

*Case insensitive (except for Table name)*
