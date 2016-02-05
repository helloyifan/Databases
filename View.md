#Views

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

