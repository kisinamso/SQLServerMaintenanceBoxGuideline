# Databases Backup Guideline

## Parameters
|***Parameter Name***|***Type***|***Optionality***|***Description***|
|------|------|-----|-----|
|@dbName|NVARCHAR(128)|Optional|Database name to backup. Default is all databases.|
|@backupType|NVARCHAR(128)|Optional|Backup type (full, diff, trn). Default is full.|
|@backupPath|NVARCHAR(128)|Mandatory|Backup path like this: 'C:\YourBackupFolder'|

Has three parameter. These are Database Name, Backup Type and Backup Path. These two optional but one of them mandatory.
1. If you will not set to database name, backup operations works for all databases.
2. If you will not set to backup type, backup type is full backup.
3. Last one is mandatory parameter and you must set backup path but it must not end with **" \ "** operator.

## Logging
This stored procedure helps to log database backup jobs. You can create with this procedure in your **Maintenance database**. And with this stored procedure, you can log database backups result.
Your backups result save to **[ENTER_DB_NAME].[dbo].[BackupLog]** table. You must change the database name but schema is optional.
**Log Table Informations**
Name: BackupLog

|***ColumnName***|***Data Type***|***Column Description***|
|------|------|-----|
|LogID|INT|Table's primary key and identity column.|
|DatabaseName|NVARCHAR(128)|Database name to backup.|
|BackupType|NVARCHAR(10)|Backup type like full, trn, diff.|
|BackupPath|NVARCHAR(256)|Backup Path like 'C\Backup'|
|BackupFileName|NVARCHAR(256)|Database Backup Name|
|BackupDateTime|DATETIME|Backup Date Time|

## Tips
1. This backup plan prepared for 3 different time sequences. Time sequences are daily, monthly and yearly. You can change according to your backup plan.
2. You can create SQL Agent Job for databases backup. All you have to do is define this stored procedure in your SQL Agent Job step.
3. This stored procedure works without backup parameters if you want to add parameters you can add the related lines. For find related lines you can use **CTRL + F** shortkey with this keywords; '**-- WITH --You can add parameter to here**'
4. If you do not want to log records over a certain period of time, you can delete the records in the  **[ENTER_DB_NAME].[dbo].[BackupLog]** table by adding the second step to the SQL Agent Job you have created. Like this:\
   |***Second Step***|
   |------|
   |DECLARE @Retention INT = -30 DELETE FROM [ENTER_DB_NAME].[dbo].[BackupLog] WHERE BackupDateTime < DATEADD(DAY,@Retention, GETDATE())|
   
## Examples

### Scenario 1
**I just want to *[XX]* database full backup. So i can execute like this:**
|Method 1| Method 2|
|------|------|
|EXEC [ENTER_DB_NAME].[dbo].[BackupDatabase] @dbName = 'XX', @backupType = 'full', @backupPath = 'C:\Backup'|EXEC [ENTER_DB_NAME].[dbo].[BackupDatabase] @dbName = 'XX', @backupPath = 'C:\Backup'|

**Let's control them.**
||
|------|
|SELECT * FROM [ENTER_DB_NAME].[dbo].[BackupLog] WITH(NOLOCK) WHERE DatabaseName = 'XX'|

### Scenario 2
**I just want to all database full backup. So i can execute like this:**
|Method 1| Method 2|
|------|------|
|EXEC [ENTER_DB_NAME].[dbo].[BackupDatabase]  @backupType = 'full', @backupPath = 'C:\Backup'|EXEC [ENTER_DB_NAME].[dbo].[BackupDatabase] @backupPath = 'C:\Backup'|

**Let's control them.**
||
|------|
|SELECT * FROM [ENTER_DB_NAME].[dbo].[BackupLog] WITH(NOLOCK)|

### Scenario 3
**I just want to *[XX]* database differantial backup. So i can execute like this:**
|Method 1|
|------|
|EXEC [ENTER_DB_NAME].[dbo].[BackupDatabase] @dbName = 'XX', @backupType = 'diff', @backupPath = 'C:\Backup'|

**Let's control them.**
||
|------|
|SELECT * FROM [ENTER_DB_NAME].[dbo].[BackupLog] WITH(NOLOCK) WHERE DatabaseName = 'XX'|

### Scenario 4
**I just want to *[XX]* database log backup. So i can execute like this:**
|Method 1|
|------|
|EXEC [ENTER_DB_NAME].[dbo].[BackupDatabase] @dbName = 'XX', @backupType = 'trn', @backupPath = 'C:\Backup'|

**Let's control them.**
||
|------|
|SELECT * FROM [ENTER_DB_NAME].[dbo].[BackupLog] WITH(NOLOCK) WHERE DatabaseName = 'XX'|

## Access The Stored Procedures
I know you wonder about this stored procedure :) Do not worry you can access with free. Click **[here](https://github.com/kisinamso/SQLServerMaintenanceBox/blob/main/002_DatabaseBackup.sql)** for access.

