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

**SELECT**: Every query must have SELECT clause, which specifies COLUMNS to be retained in the result.
- the select list is a list of (expressions involing) COLUMNS NAMES of tables named in the from list.
- columns names can be prefixed by a range variable

**FROM**: a FROM clause which specifies a cross-product on tables.
- the from-list is a list of TABLE NAMES (can be followed by a range variable)

**WHERE**: optional WHERE clause: specifes selection conditions on the tables mentioned in the FROM
- condtions 
- logical operators
- comparision operators
- boolean combination of condtions of the form of expression(s)
- **expression**: column name, constant  or an (arithmetic or string) expression

The close relationship between SQL and relational algebra is the basis for query optimization in a relational DBMS

```
SELECT DISTINCT S.sname, S.age
From Sailors S
```
This query is equivalent to applyng the the PROJECTION operator of RA

Distint: we could get a copy of rows, prevents multiset
-optional
- it indicates that the table should not complain diplicates (two copies of the same row)
- by default, duplicates are not eliminated.

Multiset: Similar to a set that is unordered collection of elements, but there could be several copies of each element
and the number of copies is significant. two multisets could have  the same elements and yet be different because the number of copies is different for some elements.


```
SELECT S.sid, S.sname, S.rating, S.age
FROM Sailors AS S
WHERE S.rating > 7
```

This query is equivalent to the SELECTION operator of ra

This query uses the OPTIONAL KEYWORD AS. to introduce a RANGE VARIABLE. 

Incidentally, when we want to retrieve all columns as  in this query, we can use (*)
(*) Is useful for interactive querying , but it is poor style for queries that are intedend to be reused and maintained because  the schema of the result is not clear from the query itself.

Recall
the SELECT clause is actually used to do projection,
whereas selections in the relational algebra sense are expressed using the WHERE clause! 

##Union, Intersect and Except

Set-manipulation constructs that extend the basic query form presented ealier.

Find the names of sailor's who have reserved both a red and a green boat.

```
select S'name 
from Sailors S, Reserves R, Boats B
where S.sid = R.sid and R.bid = B.bid and B.color = red 

union

select S'name 
from Sailors S, Reserves R, Boats B
where S.sid = R.sid and R.bid = B.bid and B.color = green
```

