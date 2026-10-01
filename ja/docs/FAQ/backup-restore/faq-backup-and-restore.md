---
title: プリザンターのDBデータをバックアップする方法とリストアする方法を知りたい
category: FAQ：バックアップ、リストア
order: '400'
status: ''
parts: ''
urlstring: faq-backup-and-restore
translationKey: faq-backup-and-restore
shortname: バックアップ,リストア,移行
created: 2019-03-29
updated: 2024-04-29
---

## 回答

「[プリザンターのDBデータを定期的にバックアップしたい](faq-backup-schedule.md)」を参照ください。

---

## 概要

DBを[バックアップ](faq-backup-schedule.md)する際には、下記のFAQを参照してください。

[プリザンターのDBデータを定期的にバックアップしたい](faq-backup-schedule.md)

DBをリストアするには、SQL Server Management Studioよりプリザンターで使用しているDBを選択し、上記で作成したバックアップファイルを元にリストアしてください。詳しくは、以下のMicrosoft社のドキュメントを参照してください。

[データベースの完全バックアップを復元する](https://docs.microsoft.com/ja-jp/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms?view=sql-server-2017#examples)

また、プリザンターの環境移行により別の環境にDBをリストアする場合には、DBのリストア後にプリザンターのバージョンアップで使用する[CodeDefiner](../../setup/codedefiner/codedefiner-command.md)を実行する必要があります。

## 関連情報

-   [FAQ：プリザンターのDBデータを定期的にバックアップしたい（SQL Server）](faq-backup-schedule.md)
-   [データベースの完全バックアップを復元する](https://docs.microsoft.com/ja-jp/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms?view=sql-server-2017#examples)
-   [CodeDefinerのコマンド一覧](../../setup/codedefiner/codedefiner-command.md)
