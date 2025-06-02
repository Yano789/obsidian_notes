## Data Definition

### Create Database and Tables
```SQL
create database if not exists university;

create table Payroll (
	UserID integer,
	Name varchar(100),
	Job varcher(100),
	Salary integer
	primary key (UserID, Car) //use only if you need a primary key!
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

