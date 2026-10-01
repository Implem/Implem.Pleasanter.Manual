---
title: 'データベースにPostgreSQLを利用している環境で、アプリケーションエラーが発生し、エクスポートできない（Syslogsに「PostgresException: 54000」という例外が記録されるケース）'
category: FAQ：バックアップ、リストア
order: '0'
status: ''
parts: ''
urlstring: faq-backup-apperror-pgexception
translationKey: faq-backup-apperror-pgexception
shortname: ''
created: 2025-09-24
updated: 2025-09-24
---

## 回答

エクスポートする列数、リンクを減らすか、分割して出力するなどして、PostgreSQLの結合後テーブルの列数上限値である32767を超えない結果に抑える必要があります。

---

## 概要

プリザンターは、エクスポート（データベースの問い合わせ）の際、テーブル間のリンク設定に応じて、テーブルの結合（JOIN）処理を行います。

テーブルに多数のリンクが設定されていると、JOINした結果の列数がPostgreSQLの結合後テーブルの列数上限値である32767を超え、プリザンターのアプリケーションエラー発生の要因となります。列数の上限値32767はPostgreSQLの仕様であり、変更することはできません。

エクスポートする列数、リンクを減らすか、分割して出力するなどして、上限値を超えない結果に抑える必要があります。

## 操作手順

以下の手順により、本FAQに該当するかを調査してください。

1.  プリザンターの[システムログを確認・取得](../operations-and-maintenance/faq-view-syslogs.md)します。
1.  「PostgresException: 54000: joins can have at most 32767 columns」なる例外が記録されているか確認します。
