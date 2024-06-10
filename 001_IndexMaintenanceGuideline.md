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
|TableName|SYSNAME|The name of the table that performs index maintenance.|
|IndexName|SYSNAME|The name of the index that performs index maintenance.|
|FragmentationPercent|FLOAT|The fragmentation Percent of the index that performs index maintenance.|
|MaintenanceCommand|NVARCHAR(MAX)|Index reorganize or rebuild script.|
|ExecutionDate|DATETIME|Execution time of the index that performs index maintenance.|

## Examples

# Scenario 1
-- I just want to **[XX]** database index maintenance. So i can execute like this:
EXEC [ENTER_DB_NAME].[dbo].[PerformIndexMaintenance] 'XX'
-- Let's control them.
SELECT * FROM [ENTER_DB_NAME].[dbo].[IndexMaintenanceResults] WITH(NOLOCK) WHERE DatabaseName = 'XX'

# Scenario 2
-- I just want to all databases index maintenance. So i can execute like this:
EXEC [ENTER_DB_NAME].[dbo].[PerformIndexMaintenance] 
-- Let's control them.
SELECT * FROM [ENTER_DB_NAME].[dbo].[IndexMaintenanceResults] WITH(NOLOCK) 

