# 🗄️ SQL Server — Quick Reference Notes

> Personal cheat sheet for common SQL Server commands.  
> Database used in examples: `HEALTHTECHDB`

---

## 1. Check If a Database Exists

```sql
SELECT *
FROM SYS.DATABASES
WHERE NAME = 'HEALTHTECHDB'
```

**What it does:** Looks inside SQL Server's system catalog to find a specific database by name.  
If a row is returned → the database exists. No rows → it doesn't.

---

## 2. Add a Foreign Key with Cascade Rules

```sql
ALTER TABLE dbo.Sales
ADD CONSTRAINT FKSalesCustomers
    FOREIGN KEY (user_id)
    REFERENCES dbo.Customers(user_id)
    ON DELETE CASCADE
    ON UPDATE CASCADE;
```

**What it does:** Links the `Sales` table to the `Customers` table via `user_id`.

| Option | Behaviour |
|---|---|
| `ON DELETE CASCADE` | If a Customer is deleted, all their Sales rows are **automatically deleted** too |
| `ON UPDATE CASCADE` | If a Customer's `user_id` changes, all matching Sales rows are **automatically updated** |

> ⚠️ **Be careful with CASCADE** — it permanently deletes/updates linked records without asking for confirmation.

---

## 3. List All Tables in the Current Database

```sql
SELECT NAME
FROM SYS.TABLES
```

**What it does:** Returns the names of every user-created table in the database you are currently connected to.

---

## 4. Get the Full Structure of a Table

```sql
EXEC sp_help CUSTOMERS
```

**What it does:** Shows everything about the `CUSTOMERS` table, including:
- All column names and their data types
- Whether columns allow NULL
- Primary keys and foreign keys
- Indexes and constraints

> 💡 Replace `CUSTOMERS` with any table name to inspect it.

---

## 📌 Quick Reference Card

| Task | Command |
|---|---|
| Check a database exists | `SELECT * FROM SYS.DATABASES WHERE NAME = '...'` |
| List all tables | `SELECT NAME FROM SYS.TABLES` |
| Inspect a table's structure | `EXEC sp_help TableName` |
| Add a Foreign Key with Cascade | `ALTER TABLE ... ADD CONSTRAINT ... FOREIGN KEY ... ON DELETE CASCADE ON UPDATE CASCADE` |

---

*Last updated: April 2026*
