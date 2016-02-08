#Chapter 5 

## 5.1 Overview

Data Manipulation Language (DML): This subset of SQL allows users to poser queries and to intert, delete, and mofity rows.

Data Definition Language (DDL): This subset of SQL supports the creation, deleteion and modification of definitions for tables and views. Integrity constraitns can be defined on tables, either when the table is created or later.

Integrity Constaints: Can be defined on tables, either when the table is created or later

Triggers and Advanced Integrity Constraints: The new SQL:1999 standard includes support for triggers, which are actions executed by the DBMS whenever changes to the database meet condtions specified in the trigger.
SQL allows the use of queries to specify complex integrity constraint specifications.

## Form of a basic SQL Query

The basic form of an SQL query is as follows:
```
SELECT [DISTINCT] select-list
FROM from-list
WHERE qualification
```

Every query must have SELECT clause, which specifies COLUMNS to be retained in the result.
a FROM clause: which specifies a cross-product on tables.
option WHERE clause: specifes selection conditions on the tables mentioned in the FROM

The close relationship between SQL and relational algebra is the basis for query optimization in a relational DBMS

```
SELECT DISTINCTT S.sname, S.age
From Sailors S
```
This query is equivalent to applyng the the PROJECTION operator of RA

Distint: we could get a copy of rows, prevents multiset
Multiset: Similar to a set that is unordered collection of elements, but there could be several copies of each element
and the number of copies is significant. two multisets could have  the same elements and yet be different because the number of copies is different for some elements.




