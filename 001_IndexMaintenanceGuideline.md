# Index Maintenance Guideline

## Parameters
| ***Parameter Name*** | ***Type*** | ***Is Optional***|
|------|------|-----|
|@DatabaseName  |SYSNAME  |Optional |

Has only one parameter. It's database name.
If this parameter set **NULL**, all online databases indexes perform rebuild or reorganize except system databases. But if **specifed a database name** perform rebuild or reorganize for only specified databases.

## Logging
This stored procedure helps to log index maintenance jobs. You can create with this procedure in your **Maintenance database**. And with this stored procedure, you can log index maintenance result.
Your index maintenance result save to **[ENTER_DB_NAME].[dbo].[IndexMaintenanceResults]** table. You must change the database name but schema is optional.
**Log Table Informations**
Name: IndexMaintenanceResults

|***ColumnName***|***Data Type***|***Column Description***|
|------|------|-----|
|ID|INT|Table's primary key and identity column.|
|DatabaseName|SYSNAME|The name of the database that performs index maintenance.|
|SchemaName|SYSNAME|The name of the schema that performs index maintenance.|
