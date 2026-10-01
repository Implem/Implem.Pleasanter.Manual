---
title: Azure上に導入したプリザンターのDBデータをバックアップする方法とリストアする方法を知りたい
category: FAQ：バックアップ、リストア
order: '100'
status: ''
parts: ''
urlstring: faq-azure-backup-restore
translationKey: faq-azure-backup-restore
shortname: ''
created: 2019-04-02
updated: 2024-04-29
---

## 回答

AzureのSQL Databaseの[バックアップ](faq-backup-and-restore.md)は、Azure上で自動的に実施されておりますので手動でのバックアップは不要です。

---

## 概要

AzureのSQL Databaseのバックアップは、Azure上で自動的に実施されておりますので手動でのバックアップは不要です。詳しくは、下記のMicrosoft社のドキュメントを参照してください。

[自動の geo 冗長バックアップ - Azure SQL Database | Microsoft Learn](https://docs.microsoft.com/ja-jp/azure/sql-database/sql-database-automated-backups)

DBのリストア手順は、下記のMicrosoft社のドキュメントを参照してください。

-   Azure Portalからの復元方法  
    [バックアップからデータベースを復元する - Azure SQL Database | Microsoft Learn](https://docs.microsoft.com/ja-jp/azure/sql-database/sql-database-recovery-using-backups)
-   SQL Server Management Studioを使用した復元方法  
    [SSMS を使用してデータベース バックアップを復元する - SQL Server | Microsoft Learn](https://learn.microsoft.com/ja-jp/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms?view=sql-server-ver16#examples)

また、バックアップ取得時とリストア後のプリザンターのバージョンが異なる場合は、プリザンターのバージョンアップ作業が必要になることがあります。バージョンアップ作業の手順は[プリザンターのバージョンアップ手順(Azure App Service)](../../setup/version-up-migration/version-up-manually/version-up-azure.md)を参照してください。

## 関連情報

-   [FAQ：プリザンターのDBデータをバックアップする方法とリストアする方法を知りたい](faq-backup-and-restore.md)
-   [FAQ：プリザンターのDBデータを定期的にバックアップしたい（SQL Server）](https://pleasanter.org/ja/manual/faq-backup-schedule)
