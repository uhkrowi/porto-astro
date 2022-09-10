---
layout: "../../layouts/BlogPost.astro"
title: "Stored Procedure"
pubDate: "Jul 08, 2022"
---

Recently I have to work with stored procedures for a pretty huge monolith project, it’s not something new for me but I’ve been leaving it for a quite long time so I need to refresh my knowledge.

To get it simplified, stored procedure is just a bunch of SQL queries that wrapped and can be executed with a single command (you can also call functions in it when you have several common tasks to run).

Anyway I don’t really like to manipulate data through neither SQL stored procedures, functions nor views, because I don’t want to separate my app logics, so I do every manipulating processes on the backend code with ORM’s query builder or a plain query if possible.

That’s not a big deal tho, if you prefer to do so, you could group the queries into a single stored procedure then execute it when needed.

Okay, now we know what do stored procedures used for, let’s get some practices.

**Creating tables and put some values**

```sql
CREATE TABLE Employee
(ID INT NOT NULL IDENTITY(1,1) PRIMARY KEY, FullName VARCHAR(100), Salary DECIMAL)
GO

CREATE TABLE EmployeeAttendance
(ID INT NOT NULL IDENTITY(1,1) PRIMARY KEY, EmployeeID INT, TimeIn DATETIME, TimeOut DATETIME)
GO

INSERT INTO Employee (FullName, Salary) VALUES ('Leo Wick', 5000)
,('Peter Potter', 4500)
,('Harry Parker', 6000)
GO

INSERT INTO EmployeeAttendance (EmployeeID, TimeIn, TimeOut) VALUES (1, '2021-02-04 09:00:00', '2021-02-04 18:00:00')
,(1, '2021-02-05 09:00:00', '2021-02-05 18:00:00')
,(1, '2021-02-06 09:00:00', '2021-02-06 18:00:00')
,(1, '2021-02-07 09:00:00', '2021-02-07 18:00:00')
,(1, '2021-02-08 09:00:00', '2021-02-08 18:00:00')
,(2, '2021-02-04 09:00:00', '2021-02-04 18:00:00')
,(2, '2021-02-05 09:00:00', '2021-02-05 18:00:00')
,(2, '2021-02-06 09:00:00', '2021-02-06 18:00:00')
,(2, '2021-02-07 09:00:00', '2021-02-07 18:00:00')
,(2, '2021-02-08 09:00:00', '2021-02-08 18:00:00')
,(3, '2021-02-04 09:00:00', '2021-02-04 18:00:00')
,(3, '2021-02-05 09:00:00', '2021-02-05 18:00:00')
,(3, '2021-02-06 09:00:00', '2021-02-06 18:00:00')
,(3, '2021-02-07 09:00:00', '2021-02-07 18:00:00')
,(3, '2021-02-08 09:00:00', '2021-02-08 18:00:00')
```

