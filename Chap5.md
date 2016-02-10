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

- IN
- By using NOT EXISTS instead of EXISTS we can compute the name of teh sailors WHO HAVE NOT RESERVED A RED BOAT.
- Closely there exists the Unique predicate (and NOT UNIQUE)

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

SQL provides a special column value called null to use in such situations. We use null when the column value is either unknown or inapplicable.
The presences of null valuse complicates many issues, and we consider the impact of null values on SQL in this section.





Literally from the textbook "The expression NOT unknown is defined to be unknown."

In the where clause: any row that evaluates to NULL of FAlse is eliminated

####5.6.1 Comparisons Using Null Values
```
rating = 8.
```
Since rating is unknown, it is resonable to say that this comparison should evaluate to the value unknown. This is the case for rating > 8 and rating < 8

Perhaps less obviously, if we compare two null values using <,>,= and so one, the result is always unknown.

SQL provides a special comparsion operator IS NULL to test whether a column valuse is null. (IS NOT NULL)

####5.6.2 Logical Connectives AND, OR, and NOT
SQL uses three-valued logc in which values evaluat to(true, false ,unknown)

The expression `NOT unknown` is defiend to be unknown.
OR 
- either is true, evalues to true
- if one unkown, one false, then its unknown

AND
- false if either false 
- if one unkown and one true or unknown , then its unknown

####5.6.3 Impact on SQL Constructs 
For example, the qualificaiton in the WHERE clause eliminates rows (in the cross-product of tables named in the FROM clause) for which the qualification does not evaluate to true.

In the presence of null values, any row that evaluates to false or unknown is eliminated.

Eliminating rows that evaluate to unknown has a subtle but significant impact on queries especically nested queries involving EXISTS or UNIQUE

Another issue: When two ruws in a relation instanec are regardes as duplicates. 

The SQL definition is that two rows are duplicates if corresponding columns are either equal orborh contain null.

Construct this definition with the fact that if we compare two null valuse using =, the result is unknown
In the context of duplicates, this comparison is implicity treated as true which is an anomaly

* Arithmetic Operations (+-*/) return null if one of their arguments is null.
* Aggreate Operations can handle null values (COUNT(*) counts it). All the other aggregate operations (COUNT, SUM, AVG,
MIN, MAX, and variations using DISTINCT) disgards null value
* Sum doesnt sum since its sill arithmetic
* Special case, with the exception of count(*) is applied to only null values, the result again is null

####5.6.4 Outer Joins

outer joins are supported in SQL.

Consider the join of two table:
ie: Joining `Sailors ⋈c Reserves`. Tuples of Sailor that do not match some row in Reserves according to the join condtion c do not appear in the result.

Outer joins on the other hand, Sailor rows without a matching Reserves row appear exactly once in the result with the result columns inherited from Reserves assigned values

Types of Outer Joins
- Left outer joins: sailor rows without a matching reserves row appear in the result, but not vice versa
- Right outer join: reserves row without matching sailors appear in the result, but not vice versa
 
In a full outer join, both Sailors and Reserves rows without a match appear in the result (ofc rows that match appear in the result as usual joins, sometimes called inner joins)

SQL allows the desired type of join t obe specified in the FROM clause.

```
SELECT S.sid, R.bid
FROM Sailor S NATURAL LEFT OUTER JOIN Reserves R
```

**Natural**: specifies that the join condion is equality on all common attributes (in this examlpe only sid) and the WHERE clause is not required (unless we want specificy addtional, non-join conditions

###5.6.6 Disallowing Null Values.

We can disallow numm valuse by specifying NOT NULL as part of the field defition

```
sname CHAR(20) NOT NULL
```

In addition primary keys are not alloed totake on null values

##5.7 Complex Integrity Constaints in SQL

SQL constraints are used to specify rules for the data in a table.

If there is any violation between the constraint and the data action, the action is aborted by the constraint.

Constraints can be specified when the table is created (inside the CREATE TABLE statement) or after the table is created (inside the ALTER TABLE statement).


###Constraints over a single table
**Check**: Conditional expression is used over a single table constaints

```
CREATE TABLE Sailors ( sid INTEGER,
sname CHAR(10),
rating INTEGER,
age REAL,
PRIMARY KEY (sid),
CHECK (rating >= 1 AND rating <= 10 ))
```

###Domain Constraint
A user can define a new domain using the CREATE DOMAIN statement, which uses check constraints
```
CREATE DOMAIN ratingval INTEGER DEFAULT 1
CHECK ( VALUE >= 1 AND VALUE <= 10 )
```

Domains: are basically datatypes with a constraint

```
CREATE TYPE ratingtype AS INTEGER
```

Defines a new distinct type called rating type, with INTEGER  type sources
Rating types can be compared with each others, but cannot be compared with values of other types. (Threated different from types)
We can use predefined operations, must do so explicitly

###Assertions: Which are Constraints over Several Tables


Table constraints are associated with a single table. Check can refer to other  tables.
Table constraints are required to hold only if the associated table is nonempty.

When a constraints involves two or mor tables. (This table constraints may not be desired)
SQL also supporsts CREATE ASSERTION  (which are constraints not associated with anyone table) to deal with this situation

Example: Constraints is number of boats plus the number of sailors should be less than 100
```
CREATE TABLE Sailors(sid integer
                     sname CHAR(10),
                     rating INTEGER,
                     age REAL,
                     PRIMARY KEY (sid),
                     CHECK((rating >=1 AND rating <= 10))
                     CHECK((SELECT COUNT (S.sid) FROM Sailor S) + (SELECT COUNT (B.Bid) FROM Boats B) < 100))
```

Draw backs:
- Associated with sailor although it involes Boats in a completely symmetric way
- If the sailrs table was empty, this constraints is defined (as per the semantics of table constraints) to always hold, even if we have more then 100 rows in boats

Better solution **Assertions**
```
CREATE ASSERTION smallClub
CHECK((SELECT COUNT (S.sid) FROM Sailor S) + (SELECT COUNT (B.Bid) FROM Boats B) < 100))
```

##5.8 Triggers and Active Databases

Trigger: A procedures that is automatically invoked by the DBMS to reponse to specified changed in the database
Active Dataase : A db that has a set of associated triggers

Event: A change to the db that activates the rigger

Condition: A query or tests that is run when the trigger is activated
- Can be a ture/false statement
- A query is interpreted as true if the answer set is nonempty and false if the query has no answer

Action: A procedures that is executed when the trigger is activated and the condition is ture
- Can examine the answers to the query in the conditon part of the trigger
- refer to old and new values of tuples modified in the statement by the activating trigger
- excute new queries and make changes to the db

Issues with trigger is we may want its actions to execute before changes are made or  maybe afterwards.
- A trigger that initializes a variable used to count the number of qualifying insertions should be executed before
- A trigger that excutes once per qualifiyng inserted record and increments the variable should be executed after each record is inserted

Example
The trigger called iniLcount initializes a counter variable before every execution of an INSERT statement that adds tuples to the Students relation. 

The trigger called incr_count increments the counter for each inserted tuple that satisfies the condition age < 18.

```
CREATE TRIGGER  initCount BEFORE INSERT ON Students
          Declare 
                    count INTEGER       /*Event* /
          BEGIN
                    count :=0;           /* ACTION */
          END
```
```
CREATE TRIGGER  incCount AFTER INSERT ON Students
          WHEN (neg.age < 18)                     /*Condition: new is just-inserted tuple* /
          FOR EACH ROW
                    count INTEGER                 
          BEGIN
                    count := count + 1;       /* ACTION: a procedures in Oracle's PL/SQL */
          END
```
