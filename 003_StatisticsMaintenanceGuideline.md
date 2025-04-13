
# 📄 StatisticsM aintenance Guideline Documentation  
> **Author:** `@kisinamso`  
> **Purpose:** Automatically update table statistics and log the process.

---

## 📌 Purpose  
Updates statistics on all tables within the specified database or all user databases.  
Each update is logged into the `StatisticsUpdateLog` table.

---

## 🧾 Input Parameters

| Parameter Name   | Type      | Description |
|------------------|-----------|-------------|
| `@DatabaseName`  | `SYSNAME` | If `NULL`, runs for all user databases. If a specific name is given, runs only for that one. |

---

## 📋 Log Table: `dbo.StatisticsUpdateLog`  
**Automatically created if it doesn't exist.**

| Column Name     | Data Type       | Description                      |
|------------------|------------------|----------------------------------|
| `LogID`          | `INT (IDENTITY)` | Auto-increment identity column   |
| `DatabaseName`   | `SYSNAME`        | Database where update was run    |
| `SchemaName`     | `SYSNAME`        | Schema of the table              |
| `TableName`      | `SYSNAME`        | Name of the table                |
| `StatisticName`  | `SYSNAME`        | Name of the updated statistic    |
| `UpdateDate`     | `DATETIME`       | Timestamp of the update          |
| `Status`         | `VARCHAR(10)`    | `'Success'` or `'Fail'`          |
| `ErrorMessage`   | `NVARCHAR(MAX)`  | Error message if any             |

---

## ⚙️ How It Works

1. If `@DatabaseName` is NULL, runs on all user databases.  
2. For each database:
    - Retrieves all tables and their statistics from `sys.stats`.
    - Generates `UPDATE STATISTICS ... WITH FULLSCAN` commands.
3. Executes each update inside a `TRY/CATCH` block.
4. Logs successful updates as `"Success"`, and failed ones as `"Fail"`.

---

## 🔁 Used Structures

- **Cursor 1**: `db_cursor` → Iterates through user databases.  
- **Cursor 2**: `table_cursor` → Iterates through table statistics in each database.  
- **Dynamic SQL**: Uses `sp_executesql` to execute the `UPDATE STATISTICS` command.

---

## ⚠️ Security & Performance Notes

- Requires elevated privileges; should only be run by authorized users.  
- `WITH FULLSCAN` provides more accurate stats but may be time-consuming.

---

## 📈 Monitoring & Enhancement Suggestions

- Can be scheduled using SQL Server Agent Job for periodic execution.  
- The `StatisticsUpdateLog` table can be visualized via Power BI, SSRS, or other tools.  
- Logged entries enable historical review and auditability.

---
