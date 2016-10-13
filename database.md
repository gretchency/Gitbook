# Database

SQL Injection

The only proven way to protect a web site from SQL injection attacks, is to use **SQL parameters**.

```java
txtUserId = getRequestString("UserId");
txtSQL = "SELECT * FROM Users WHERE UserId = @0";
db.Execute(txtSQL,txtUserId);
```

SQL Select Top 5

MySQL syntax
```java
SELECT *
FROM Persons
LIMIT 5;
```

SQL LIKE Operation

The following SQL statement selects all customers with a City starting with the letter "s":
```java
SELECT * FROM Customers
WHERE City LIKE 's%';
```

The following SQL statement selects all customers with a City ending with the letter "s":
```java
SELECT * FROM Customers
WHERE City LIKE '%s';
```


