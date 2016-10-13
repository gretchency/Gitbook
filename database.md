# Database

SQL Injection

The only proven way to protect a web site from SQL injection attacks, is to use **SQL parameters**.

```java
txtUserId = getRequestString("UserId");
txtSQL = "SELECT * FROM Users WHERE UserId = @0";
db.Execute(txtSQL,txtUserId);
```