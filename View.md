#Views

A view is a table whose rows are not explicitly stored in the database but are computed as needed from a view definition

```
CREATE VIEW B-Students (name, sid, course)
  AS SELECT S.sname, S.sid, E.cid
  FROM Students S, Enrolled E
  WHERE S.sid = E.studid AND E,grade = 'B'
```
