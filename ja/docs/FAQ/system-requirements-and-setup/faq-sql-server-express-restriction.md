---
title: SQL Server Expressの制約について教えてください。
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-sql-server-express-restriction
translationKey: faq-sql-server-express-restriction
shortname: ''
created: 2025-06-12
updated: 2026-01-13
---

## 回答

SQL Server Expressは無料で使用できるSQL Serverのエディションです。プリザンター使用において機能面での制約はありませんが、利用可能なリソース上限などの制限があります。

---

## 概要

SQL Server Expressには以下の制約があります。特にデータベースの使用量が下記の制限値を超えるとデータの書き込みでエラーが発生する他、ログイン画面が表示できなくなる恐れがあります。またメモリ、CPUの上限によりサーバが高スペックであっても期待したパフォーマンスが発揮できない恐れがあります。

### リソース

SQL Server Expressを導入するサーバが高スペックであっても、以下の制限を超えたリソースを使う事ができません。

| リソース         | 制限値                                                                   |
| ---------------- | ------------------------------------------------------------------------ |
| データベース容量 | SQL Server 2025 Express以降：50 GB<br>SQL Server 2022 Express以前：10 GB |
| メモリ容量       | 1410MB                                                                   |
| CPU              | 1物理CPUまたは4コアの小さいほう                                          |

### メンテナンスプラン

[SQL Server Expressではメンテナンスプランが使用できない](https://learn.microsoft.com/ja-jp/troubleshoot/sql/database-engine/backup-restore/schedule-automate-backup-database)ため、メンテナンスプランを利用した「データベースの定期バックアップ」ができません。SQL Server Expressを使用した場合で定期バックアップを行う際は以下ページを参照ください。
[プリザンターのデータベース(SQL Server)をバックアップする](../../setup/additional/db-server/backup-sql-server.md)

### 詳細情報

その他詳細については以下のMicrosoft公式ページを参照ください。

-   [SQL Server 2025 のエディションとサポートされている機能 \- SQL Server \| Microsoft Learn](https://learn.microsoft.com/ja-jp/sql/sql-server/editions-and-components-of-sql-server-2025)
-   [SQL Server 2022 のエディションとサポートされている機能 \- SQL Server \| Microsoft Learn](https://learn.microsoft.com/ja-jp/sql/sql-server/editions-and-components-of-sql-server-2022?view=sql-server-ver16)
-   [SQL Server 2019 の各エディションとサポートされている機能 \- SQL Server \| Microsoft Learn](https://learn.microsoft.com/ja-jp/sql/sql-server/editions-and-components-of-sql-server-2019?view=sql-server-ver15)
-   [エディションとサポートされる機能 \- SQL Server 2017 \| Microsoft Learn](https://learn.microsoft.com/ja-jp/sql/sql-server/editions-and-components-of-sql-server-2017)
