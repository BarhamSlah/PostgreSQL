# Part 10 — PostgreSQL with Java

**Target time:** 4 hours  
**Goal:** Understand the normal path from a Java application to PostgreSQL using JDBC.

This part assumes you already understand basic Java classes, exceptions, and SQL CRUD.

## 1. What is JDBC?

JDBC (Java Database Connectivity) is the standard Java API for connecting to relational databases and sending SQL statements.

The PostgreSQL JDBC driver (pgJDBC) allows Java applications to communicate with PostgreSQL.

## 2. The basic flow

1. Add the PostgreSQL JDBC driver to your project.
2. Create a database connection.
3. Prepare an SQL statement.
4. Set parameter values.
5. Execute the statement.
6. Read results when the query returns rows.
7. Close resources.

## 3. The main JDBC types

| Type | Role |
|---|---|
| Connection | Represents a database connection |
| PreparedStatement | Executes parameterized SQL |
| ResultSet | Reads rows returned by a query |
| SQLException | Represents database access errors |

## 4. Why PreparedStatement?

Use parameters instead of joining user input into SQL strings. This helps prevent SQL injection and handles values correctly.

Conceptual example:

```java
String sql = "SELECT * FROM customers WHERE email = ?";
PreparedStatement statement = connection.prepareStatement(sql);
statement.setString(1, email);
ResultSet result = statement.executeQuery();
```

The question mark is a parameter placeholder. The value is supplied separately.

## 5. Which execution method?

- `executeQuery()`: for queries that return a ResultSet, commonly SELECT.
- `executeUpdate()`: for INSERT, UPDATE, DELETE, and many DDL statements; returns an update count.
- `execute()`: for statements where the result type may vary.

## 6. Resource management

Use try-with-resources so Connection, PreparedStatement, and ResultSet are closed reliably. Do not hard-code real database passwords in a public GitHub repository. Use environment variables or a secure configuration mechanism.

## Practice tasks

1. Add the pgJDBC dependency to a small Java project.
2. Connect to your local `postgres_learning` database.
3. Select and display records.
4. Insert a record using PreparedStatement.
5. Update a record using PreparedStatement.
6. Delete a test record using PreparedStatement.
7. Handle SQLException and close resources safely.

## Checklist

- [ ] I understand what JDBC does.
- [ ] I know the roles of Connection, PreparedStatement, and ResultSet.
- [ ] I can explain why PreparedStatement is important.
- [ ] I know executeQuery vs executeUpdate.
- [ ] I do not publish database credentials.
## Understand the connection flow

```text
Java application
      |
      | JDBC API
      v
PostgreSQL JDBC driver (pgJDBC)
      |
      v
PostgreSQL database
```

JDBC is the Java API; pgJDBC is the driver that lets Java communicate with PostgreSQL. You need both: JDBC types in your Java code and the PostgreSQL driver dependency in your project.

## Understand the three most-used JDBC objects

- **Connection:** an active connection to the database.
- **PreparedStatement:** a SQL statement with placeholders for values.
- **ResultSet:** the rows returned by a query such as SELECT.

### Why the question mark matters

In `WHERE email = ?`, the question mark is a parameter placeholder. Calling `setString(1, email)` supplies the first parameter. The value is sent separately from the SQL structure, which helps prevent SQL injection and handles quoting safely.

Do not build SQL by joining user input into the query string.

## Choose the execution method

| Method | Use it for | What it returns |
|---|---|---|
| executeQuery() | A query that returns rows, usually SELECT | ResultSet |
| executeUpdate() | INSERT, UPDATE, DELETE and many DDL statements | Number of affected rows (or 0 for statements without a row count) |
| execute() | When the result type may vary | A boolean indicating whether the first result is a ResultSet |

## Keep credentials private

Never commit real passwords, API keys or private connection strings to GitHub. Use environment variables or a secure configuration method. If a password was accidentally committed, changing the file later does not make the old secret safe; rotate the exposed credential.
