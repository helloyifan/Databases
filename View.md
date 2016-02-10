#Views

Definition View:
A view is a relation in the external schema whose instance is determined by the instances of the relations in the conceptual schema.

---

A view is a table whose rows are not explicitly stored in the database but are computed as needed from a view definition

```
CREATE VIEW B-Students (name, sid, course)
  AS SELECT S.sname, S.sid, E.cid
  FROM Students S, Enrolled E
  WHERE S.sid = E.studid AND E,grade = 'B'
```

The view B-Studnets has three fields called name, sid, and course with the same domains as the fields sname and sid in Student and cid in Enrolled.

If the optional arguments name, sid, and course are ommited from the CREATE VIEW statement, the column names sname, sid and cid are inherited

This veiw can be used just like a base talble in defining new queries or views

When View is used in a query, the view definition is first evaluated to obtain the corresponding instance of B-studets, then the rest of the query is evaluated treating B-students like any other relation referred to in the query

Views provide the support for logical data independence in the relational model

Views are also valuable in the context of security. We can defined view that give a group of users access to just the information they are allowed to see

##Updates on Views

The motivation behind the veiw mechanism is to tailor how users see the data. User's should not hve to worry about the view versus base table distictintion.

The goal is inedeedto achieved in the cause of queries on views, a view can be used just like any other relation in defining a query. However it is natual to want to specify updates on views as well.


The SQL 92 standard allows updates to be specified only on views that are defiend on a single base table using just selection and projection with no use of aggreate operations

Such views are called updateable view

An updates on such a restircted view can always be implemented by updating the underlying base table in an unambiguous way. Consider the following view

```
CREATE VIEW GoodStudent (sid, gpa)
  AS SELECT S.sid S.gpa
  FROM STUDENTS S
  WHERE S.gpa > 3.0
```

We can implement a comand to modify the gpa of a GoodStudents row by modifying the corresponding row in Students. 
We can delete a GoodStudents row bt delteing the corresponding row in student

While the SQL rules on updateable views are more stric than necessary there are some fundamental problems with updates specified on views and good reaon to limit the class of views that can be updated...

We can insert a GoodStudents row by inserting a row into students, using null valuse in Columns of student that do not appear in GoodStudents (sname, Login)

##updating External Schmea is difficult

