# Databases Backup Guideline

## Parameters
|***Parameter Name***|***Type***|***Optionality***|***Description***|
|------|------|-----|-----|
|@dbName|NVARCHAR(128)|Optional|Database name to backup. Default is all databases.|
|@backupType|NVARCHAR(128)|Optional|Backup type (full, diff, trn). Default is full.|
|@backupPath|NVARCHAR(128)|Mandatory|Backup path like this: 'C:\YourBackupFolder'|
