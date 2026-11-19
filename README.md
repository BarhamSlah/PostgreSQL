# PostgreSQL Practical Learning

A hands-on, beginner-friendly path to using **PostgreSQL and the `psql` command-line tool** confidently for everyday database work and Java backend projects.

> **Target:** 30–35 focused hours. This is a practical foundation, not a database-administrator course and not a guarantee of job readiness.

## How to study

Study in repository order. For each lesson:

1. Read the explanation and understand the purpose.
2. Open **SQL Shell (psql)** and connect to your practice database.
3. Type and run the examples yourself. Do not only read or copy them.
4. Complete the exercises without looking at solutions.
5. Check the lesson checklist before moving on.
6. Use a video only when you need another explanation of a specific topic.

**Suggested pace:** 45–60 minutes per study session. You can spend more than one session on a difficult lesson. Understanding matters more than finishing quickly.

## Learning roadmap

| Part | Topic | Target time |
|---|---|---:|
| [01](./01-Getting-Started/README.md) | Getting started: PostgreSQL, psql, connecting, navigation | 2 hours |
| [02](./02-SQL-Basics/README.md) | Create tables and CRUD | 4 hours |
| [03](./03-Filtering-and-Sorting/README.md) | WHERE, operators, sorting, limits | 3 hours |
| [04](./04-Data-Types-and-Constraints/README.md) | Data types, keys, constraints, NULL | 3 hours |
| [05](./05-Relationships-and-Joins/README.md) | Relationships and JOINs | 5 hours |
| [06](./06-Aggregation/README.md) | Aggregate functions, GROUP BY, HAVING | 2 hours |
| [07](./07-Useful-Query-Techniques/README.md) | CASE, subqueries, CTE introduction | 2 hours |
| [08](./08-Everyday-Database-Management/README.md) | ALTER, transactions, indexes, backup basics | 4 hours |
| [09](./09-Practical-Projects/README.md) | Build and query realistic databases | 6 hours |
| [10](./10-PostgreSQL-with-Java/README.md) | JDBC and safe database access | 4 hours |
| | **Total** | **35 hours** |

Times are estimates. Repeat exercises when needed.

## Important: SQL vs psql

They are related, but they are not the same:

- **PostgreSQL** is the database system.
- **SQL** is the language used to create, read, change, and delete data.
- **psql** is a terminal program for connecting to PostgreSQL and running SQL.
- **pgAdmin 4** is a graphical tool for working with PostgreSQL.

Examples of psql meta-commands (they start with a backslash):

| Command | What it does |
|---|---|
| `\l` | List databases |
| `\c database_name` | Connect to a database |
| `\dt` | List tables in the current search path |
| `\d table_name` | Describe a table |
| `\dn` | List schemas |
| `\du` | List roles/users |
| `\conninfo` | Show connection information |
| `\q` | Exit psql |
| `\?` | Help for psql commands |
| `\h SELECT` | Help for SQL syntax |

A psql command is not SQL: do not add a semicolon to commands such as `\dt`.

## Practice database

Use one small database throughout the lessons so the examples connect together.

1. Create a database named `postgres_learning`.
2. Follow Part 02 to create the first tables.
3. Use the same tables for filtering, JOINs, aggregation, and projects.
4. Keep practice data separate from real or important databases.

Before running `UPDATE` or `DELETE`, first run a SELECT with the same WHERE condition to confirm which rows will be affected.

## What you should be able to do at the end

- Connect to a PostgreSQL server using psql.
- Create databases and relational tables.
- Insert, read, update, and delete records safely.
- Filter and sort query results.
- Use primary keys, foreign keys, and common constraints.
- Write INNER JOIN and LEFT JOIN queries.
- Group data and calculate totals and averages.
- Make basic schema changes.
- Use transactions and understand when indexes help.
- Build a small database project and connect it to Java using JDBC.

## What is intentionally not a priority

Do not spend your first learning hours on replication, high availability, deep server tuning, complex query-plan optimization, stored-procedure programming, or database administration. These topics can wait until a real project requires them.

## Learning rules

- Type SQL yourself in psql.
- Use clear table and column names.
- End SQL statements with a semicolon.
- Use single quotes for text values.
- Never use UPDATE or DELETE without checking the WHERE condition.
- Do not memorize every command; learn how to find and use the right command.
- If something fails, read the full error message and identify the line/column or object involved.

## Progress checklist

- [ ] Part 01 — Getting Started
- [ ] Part 02 — SQL Basics
- [ ] Part 03 — Filtering and Sorting
- [ ] Part 04 — Data Types and Constraints
- [ ] Part 05 — Relationships and JOINs
- [ ] Part 06 — Aggregation
- [ ] Part 07 — Useful Query Techniques
- [ ] Part 08 — Everyday Database Management
- [ ] Part 09 — Practical Projects
- [ ] Part 10 — PostgreSQL with Java

**Finish line:** You can complete the exercises and project tasks without following a tutorial line by line. Looking up syntax is normal, even for experienced developers.
