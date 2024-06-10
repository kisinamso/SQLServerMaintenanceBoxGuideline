# Database Management Scripts Guideline

This repository contains various T-SQL stored procedures guidelines that can be used for database management tasks.

## Contents

1. [Index Maintenance Guideline](001_IndexMaintenanceGuideline.md)
2. [Databases Backup Guideline](002_DatabaseBackupGuideline.md)
3. [Statistics Update Maintenance Guideline](003_StatisticsMaintenanceGuideline.md)
4. [Shrink All Databases Log Files Guideline](004_ShrinkAllLogFiles.md)
5. [Database Integrity Check Guideline](005_IntegrityCheckGuideline.md)
6. [Send Job Failure Report E-Mail Guideline](006_SendJobFailureReportGuideline.md)
7. [Blocking Check And Send E-Mail Guideline](007_BlockingCheckAndSendEmailGuideline.md)
8. [Analyzing Tables For Archiving Guideline](008_AnalyzeTablesToBeArchivedGuideline.md)

## Index Maintenance Guideline

This stored procedure performs maintenance on indexes in specified or all databases. It checks index fragmentation and reorganizes or rebuilds indexes as needed.
For details click [here](001_IndexMaintenanceGuideline.md)

## Databases Backup Guideline

This stored procedure backs up specified or all databases. It offers options for full, differential, and transaction log backups.
For details click [here](002_DatabaseBackupGuideline.md)

## Statistics Update Maintenance Guideline

This stored procedure performs maintenance on statistics in specified or all databases.
For details click [here](003_StatisticsMaintenanceGuideline.md)

## Shrink All Databases Log Files Guideline

This stored procedure aims to shrink all database log files.
For details click [here](004_ShrinkAllLogFiles.md)

## Database Integrity Check Guideline

This stored procedure checks the integrity of a specified database. If not specified, it checks the integrity of all databases.
For details click [here](005_IntegrityCheckGuideline.md)

## Send Job Failure Report E-Mail Guideline

This stored procedure sending e-mail for failured job.
For details click [here](006_SendJobFailureReportGuideline.md)

## Blocking Check And Send E-Mail Guideline

This stored procedure sending e-mail for blocking session.
For details click [here](007_BlockingCheckAndSendEmailGuideline.md)

## Analyzing Tables For Archiving Guideline

This stored procedure analyzing tables for archiving in specified or all databases.
For details click [here](008_AnalyzeTablesToBeArchivedGuideline.md)
