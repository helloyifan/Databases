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

**UNION OR**

Find the names of sailor's who have reserved both a red or a green boat.

```
select S'name 
from Sailors S, Reserves R, Boats B
where S.sid = R.sid and R.bid = B.bid and B.color = red 

union

select S'name 
from Sailors S, Reserves R, Boats B
where S.sid = R.sid and R.bid = B.bid and B.color = green
```

**INTERCEPT AND**

Find the names of sailor's who have reserved both a red and a green boat.

```
select S'name 
from Sailors S, Reserves R, Boats B
where S.sid = R.sid and R.bid = B.bid and B.color = red 

INTERESECT

select S'name 
from Sailors S, Reserves R, Boats B
where S.sid = R.sid and R.bid = B.bid and B.color = green
```
**EXCEPT NOT**

Find the names of sailor's who have reserved both a red BUT NOT a green boat.

```
select S'name 
from Sailors S, Reserves R, Boats B
where S.sid = R.sid and R.bid = B.bid and B.color = red 

EXCEPT

select S'name 
from Sailors S, Reserves R, Boats B
where S.sid = R.sid and R.bid = B.bid and B.color = green
```

##5.4 Nested Queries

- Nesting of queries is a feature that is not in RA.
- Nestest queries can be transltaed into algebra.
- Nesting in SQL is inspired more by relational calculus than algebra
- Nesting is very expressive construct 

Find the names of sailors who have reserved boat 103.

```
select s.name
from sailors s
where (   select r.bid 
          where reserves r
          where r.bid = 103)
```

**Correlation**: The occurence of a range variable in a subquery.
**Correlated Queries**:  A query that uses values from the outer query.

-IN
-By using NOT EXISTS instead of EXISTS we can compute the name of teh sailors WHO HAVE NOT RESERVED A RED BOAT.
-Closely there exists the Unique predicate (and NOT UNIQUE)

###Set-Comparison Operators

SQL supports Any and  All with comparison operators {<, <=, =, <>, >=, >}.

Find sailors whose rating is better than every sailor' called Horat·to.
```
Select S.name
from Sailors S
where S.rating > All(

select s1.rating
from sailors s1
where s1.name = 'HORATIO'
)
```

Find the 8ailor's with the highest rating.

```
Select S.name
from Sailors S
where S.rating >= All{

select s1.rating
from  sailors s1
}
```
The outer where is only satisfied only when S.rating is greater than or equal TO EACH OF THESE CONDITIONS

In is not equivalent to = ANY
Not in is not equivalent to <> ALL

##5.5 Aggregate Operators

1. COUNT: The number of uniquie values in A column;
2. SUM: The sum of all uniquie values
3. AVG
4. MAX
5. MIN

Note: It does not make sense to specify DISTINCT in conjuction with MIN or MAX but it does with the others

RA and SQL: Aggregation is a fundamental operation that cannot be expressed in RA
Similarly SQL's grouping construct cannot be expressed in algebra.


### GROUP BY and HAVING Clauses

Purpose of grouping is to avoid writing the same queries when only needing to change one variable
```
SELECT [ DISTINCT] select-list
FROM from-list
WHERE 'qualification
GROUP BY grouping-list
HAVING group-qualification
```

Find the age of the youngest sailor for each rating level.

```
select S.rating , Min (S.age)
from Sailors.S
Group by S.rating
```

The fourth step is to sort the table according to the GROUP BY caluse to identify the group
The fifth step is to apply the group-qualifications in the HAVING clause that is the codition
- ie: COUNT (*) > 1
- This step eliminates the group that dont meet this condition

The sixth step is to generate one answer row for each remaining group.
-The answer row orresponding to a group consitst of a subset of the grouping columns, plus one or more columns generated by applying an aggregating operator.

SQL 1999: Added EVERY and ANY  when used ing ht HAVING clause.

FOR each red boat; find the number of reservations for this boat.

```
select b.bid, count(*)
from Boat B, Reserves R
where B.color = 'red', B.bid = R.bid 
Group-by b.bid
```
Find the average age of sailorTs for each rating level that has at least two sailors.
```
select s.rating, avg(s.age)
from Sailors s.
Group-by s.rating
Having count(*) > 1
```

RA and SQL: Null values are not part of the basic relational model.
Tis is a depatures from the basic model

##5.6 Null Values

