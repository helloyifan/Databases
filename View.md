#Views

A view is a table whose rows are not explicitly stored in the database but are computed as needed from a view definition

```
CREATE VIEW B-Students (name, sid, course)
  AS SELECT S.sname, S.sid, E.cid
```
