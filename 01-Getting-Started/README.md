# Part 01 — Getting Started

**Goal:** Connect to PostgreSQL and understand the essential commands.

## 1. Understand the tools

| Tool | Purpose |
|---|---|
| **PostgreSQL** | The database system that stores and manages your data. |
| **SQL** | The language used to create, read, update, and delete data. |
| **psql** | A terminal program used to send SQL commands to PostgreSQL. |
| **pgAdmin 4** | A graphical tool for managing PostgreSQL. |

## 2. Connect using SQL Shell (psql)

SQL Shell asks for these connection details:

| Setting | What it means |
|---|---|
| Server | The computer running PostgreSQL. For a local installation, usually `localhost`. |
| Database | The database to connect to. Usually `postgres` for your first connection. |
| Port | The PostgreSQL connection port. Usually `5432`. |
| Username | The PostgreSQL role you want to connect as. Often `postgres`. |
| Password | The password for that PostgreSQL role. |

Press **Enter** to accept a displayed default. When you type your password, psql normally does not show the characters.

A successful connection may show:

```text
postgres=#
```

The prompt can look different depending on the database and role. The `#` commonly indicates a superuser; `>` commonly indicates a normal role.

## 3. Essential psql commands

These commands help you inspect databases, tables, schemas, users, and your connection.

| Command | Simple explanation / Benefit |
|---|---|
| `\l` | Helps you see all the databases you have. |
| `\c postgres` | Takes you to the `postgres` database so you can work inside it. |
| `\dt` | Helps you see all the tables in your current database. |
| `\d table_name` | Helps you see how a table is built, including its columns and data types. |
| `\dn` | Helps you see how your database is organized. |
| `\du` | Helps you know who can access or manage your database. |
| `\conninfo` | Helps you check which database and user you are currently connected with. |
| `\q` | Closes psql when you finish working. |
| `\?` | Helps you find psql commands when you need them. |
| `\h CREATE TABLE` | Helps you learn how to write the `CREATE TABLE` SQL command correctly. |

**Important:** These are psql meta-commands, not SQL statements. They start with a backslash and normally do not need a semicolon.

## 4. Essential SQL commands

SQL commands let you ask PostgreSQL for information.

| SQL command | What it tells you |
|---|---|
| `SELECT version();` | Shows the installed PostgreSQL version. |
| `SELECT current_database();` | Shows the database used by your current session. |
| `SELECT current_user;` | Shows the role used by your current connection. |
| `SELECT now();` | Shows the current date and time according to the server. |

**Important:** SQL statements normally end with a semicolon (`;`).

## 5. Create and connect to your practice database

Create a database:

```sql
CREATE DATABASE postgres_learning;
```

Connect to it:

```text
\c postgres_learning
```

## 6. Useful extra psql commands

| Command | What it does / Benefit |
|---|---|
| `\! cls` | Clears the Windows terminal screen. |
| `\r` | Clears an unfinished SQL query from psql's buffer. |
| `\timing` | Turns query execution-time display on or off. |
| `\x` | Switches between normal and expanded row display. |

**Do not confuse these two:**
- `\! cls` clears what you see on the screen.
- `\r` clears the unfinished SQL command you are entering.

## 7. Practice

1. Connect to the `postgres` database.
2. Check the PostgreSQL version.
3. List all databases.
4. Create `postgres_learning`.
5. Connect to `postgres_learning`.
6. Check the current database and user.
7. Exit psql and connect again.

## 8. Common problems

| Problem | What to check |
|---|---|
| Password authentication failed | Make sure you enter the password for the PostgreSQL role, not your Windows account password. |
| Connection refused | Check that the PostgreSQL server is running and that the server address and port are correct. |
| SQL command does not run | Check that the SQL statement ends with a semicolon. |
| Prompt shows `-#` | psql may be waiting for you to finish an unfinished SQL statement. Enter `;` to finish it or use `\r` to clear it. |

## 9. Understand what happens when you connect

A PostgreSQL server can contain many databases. You connect using a role (user) and select one database for your session.

```text
You → SQL Shell (psql) → PostgreSQL server → Selected database
                         ← Query result ←
```

**Remember:** psql is the client you use; PostgreSQL is the database system that processes your commands.

## 10. Connect psql to your database

When you create a database, it is stored on the PostgreSQL server. To connect your psql terminal to that database, use the `\\c` command.

## Checklist

- [ ] I can connect using SQL Shell (psql).
- [ ] I understand the difference between PostgreSQL, SQL, and psql.
- [ ] I can list databases and connect to a database.
- [ ] I can list tables, schemas, and roles.
- [ ] I can check my current connection.
- [ ] I can exit psql and reconnect.
