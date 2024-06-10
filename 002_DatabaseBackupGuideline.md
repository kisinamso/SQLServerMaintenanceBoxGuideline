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
3. Last one is mandatory parameter and you must set backup path but it must not end with "** \ **" operator.
