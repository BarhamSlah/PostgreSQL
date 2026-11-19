# PostgreSQL — Learn It Without Needing an AI Explanation

A practical, step-by-step guide to learning **SQL, PostgreSQL, and the psql terminal** for everyday database work and Java backend development.

**This repository is designed to teach each topic by itself.** You should not need to search for another explanation every time you meet a new command. Each lesson explains what a concept means, why it exists, how to use it, what to expect, common mistakes, and how to practise it.

> **Target:** About 35 focused hours. This is an everyday SQL/PostgreSQL foundation, not an advanced database-administration course.

## Start here

1. Open [Part 01 — Getting Started](./01-Getting-Started/README.md).
2. Follow the lessons in order. Later lessons use ideas from earlier ones.
3. Keep SQL Shell (psql) open and use the practice database `postgres_learning`.
4. Read the explanation before running each command.
5. Run the example, compare your result with the expected result, then try the exercise.
6. Do not move on just because you watched or read the lesson. Move on when you can explain what the query does in simple words.

## What every lesson should teach you

For each important command or concept, look for these six things:

| Part | Question it answers |
|---|---|
| Meaning | What is it? |
| Purpose | Why do we need it? |
| Syntax | What is the general command structure? |
| Example | How do I use it in a real query? |
| Result | What should I expect to happen? |
| Mistakes | What commonly goes wrong, and how do I fix it? |

If you cannot explain a command yet, return to its **Meaning** and **Example** sections. You do not need to memorize every syntax detail.

## Learning roadmap

| Part | Topic | Target time |
|---|---|---:|
| [01](./01-Getting-Started/README.md) | PostgreSQL, SQL, psql, connection and navigation | 2 hours |
| [02](./02-SQL-Basics/README.md) | Tables and CRUD: INSERT, SELECT, UPDATE, DELETE | 4 hours |
| [03](./03-Filtering-and-Sorting/README.md) | WHERE, operators, text search, NULL, sorting | 3 hours |
| [04](./04-Data-Types-and-Constraints/README.md) | Data types, primary/foreign keys and constraints | 3 hours |
| [05](./05-Relationships-and-Joins/README.md) | Relationships and JOINs | 5 hours |
| [06](./06-Aggregation/README.md) | COUNT, SUM, AVG, GROUP BY and HAVING | 2 hours |
| [07](./07-Useful-Query-Techniques/README.md) | CASE, COALESCE, subqueries and CTEs | 2 hours |
| [08](./08-Everyday-Database-Management/README.md) | ALTER, transactions, indexes and backup basics | 4 hours |
| [09](./09-Practical-Projects/README.md) | Practical database projects | 6 hours |
| [10](./10-PostgreSQL-with-Java/README.md) | JDBC and connecting PostgreSQL to Java | 4 hours |

Times are estimates. Spend extra time on a difficult topic instead of rushing.

## First understand these four names

| Name | What it is | Simple comparison |
|---|---|---|
| **SQL** | A query language for relational databases | The language you use |
| **PostgreSQL** | A relational database management system (RDBMS) | The database system |
| **psql** | A command-line client for PostgreSQL | A terminal tool to send SQL commands |
| **pgAdmin 4** | A graphical client for PostgreSQL | A visual tool to manage the database |

SQL and psql are not the same. SQL statements usually end with `;`. psql meta-commands start with `\\` and usually do not need a semicolon.

## Your practice database

Use one separate database for all lessons:

```sql
CREATE DATABASE postgres_learning;
```

Connect to it in psql:

```text
\\c postgres_learning
```

Keep your exercises inside this database. Do not practise destructive commands on important databases.

## How to understand a SQL query

Read a query from the data source to the result:

```sql
SELECT full_name, age
FROM students
WHERE age >= 18
ORDER BY age DESC;
```

- `SELECT full_name, age`: choose which columns to display.
- `FROM students`: get the data from the students table.
- `WHERE age >= 18`: keep only rows where age is at least 18.
- `ORDER BY age DESC`: show the highest ages first.
- `;`: finish the SQL statement.

Think of a query as a question you ask the database. The database returns the rows that match that question.

## A simple method for fixing errors

When a query fails, do not immediately rewrite everything.

1. Read the complete error message.
2. Find the line and position mentioned by PostgreSQL.
3. Check spelling of table and column names.
4. Check quotes: text values use single quotes, such as `'Sara'`.
5. Check that SQL statements end with `;`.
6. Check that the table exists in the database you are connected to: use `\\dt`.
7. Check the table structure: use `\\d table_name`.
8. Fix one problem, run the query again, and read the new result.

### Common psql situations

| What you see | Meaning | What to do |
|---|---|---|
| `postgres_learning=#` | Ready for a command | Type SQL or a psql command |
| `postgres_learning-#` | The previous SQL statement is incomplete | Finish it with `;`, or cancel the query with `\\r` |
| `relation does not exist` | Table name is wrong, or table is not in the current schema | Check `\\dt`, spelling and current database |
| `column does not exist` | Column name is wrong or unavailable in that query | Check `\\d table_name` |
| `syntax error` | SQL structure is invalid | Check the reported position, commas, quotes and keywords |
| `password authentication failed` | PostgreSQL rejected the role/password combination | Check the PostgreSQL username and its password |

On Windows, clear the psql screen with `\\! cls`. Clear the unfinished query buffer with `\\r`. They do different things.

## What you should be able to do at the end

- Connect to PostgreSQL with psql.
- Create databases and tables.
- Insert, read, update and delete records.
- Filter and sort query results.
- Use data types, primary keys, foreign keys and constraints.
- Join related tables.
- Calculate totals, counts and averages.
- Make basic table changes.
- Use transactions safely and understand basic indexes.
- Build a small database and connect it to Java with JDBC.

## What you can ignore for now

Do not spend your first learning hours on replication, high availability, deep server tuning, complex query-plan optimization, advanced stored procedures, or database administration. Learn these later if a project or job requires them.

## Progress checklist

- [ ] [Part 01 — Getting Started](./01-Getting-Started/README.md)
- [ ] [Part 02 — SQL Basics](./02-SQL-Basics/README.md)
- [ ] [Part 03 — Filtering and Sorting](./03-Filtering-and-Sorting/README.md)
- [ ] [Part 04 — Data Types and Constraints](./04-Data-Types-and-Constraints/README.md)
- [ ] [Part 05 — Relationships and JOINs](./05-Relationships-and-Joins/README.md)
- [ ] [Part 06 — Aggregation](./06-Aggregation/README.md)
- [ ] [Part 07 — Useful Query Techniques](./07-Useful-Query-Techniques/README.md)
- [ ] [Part 08 — Everyday Database Management](./08-Everyday-Database-Management/README.md)
- [ ] [Part 09 — Practical Projects](./09-Practical-Projects/README.md)
- [ ] [Part 10 — PostgreSQL with Java](./10-PostgreSQL-with-Java/README.md)

**Finish line:** You can solve the project requirements, explain why your queries work, and find syntax when needed. Looking up syntax is normal—even experienced developers do it.
