---
title: プリザンターのログを削除したい
category: FAQ：運用、メンテナンス
order: '0'
status: ''
parts: ''
urlstring: truncate-syslogs
translationKey: truncate-syslogs
shortname: ログの削除
created: 2021-08-27
updated: 2024-04-29
---

## 回答

1. [BackgroundService.json](../../setup/parameters/background-service-json.md)の「DeleteSysLogs」を設定する
1. SQLにて削除。本ページで説明します。

---

## 概要

プリザンターの「ログ」を削除する手順です。利用状況によってログが肥大化することがございますので、必要に応じてログの削除をご検討ください。ログの削除によるプリザンターへの動作影響はございません。

## 注意事項

1. 本手順はデータベースを直接操作するため、危険が伴います。事前に「バックアップ」を取得することを強くお勧めします。

## 操作手順

1. プリザンターをインストールしているサーバにログインします。
1. [SSMS](../../setup/installation/install-database/install-sql-server-management-studio.md)（SQL Server Management Studio）を起動します。
1. 「オブジェクトエクスプローラ」から「データベース」を展開し「Implem.Pleasanter」を選択 → 右クリック → 「新しいクエリ」をクリックします。
1. 下記「1. 削除用SQL」を実行しすべてのログを削除します。
1. 下記「2. 削除後確認用SQL」を実行しログが削除されていることを確認する。

## サンプルコード

### 1. 削除用SQL

##### SQL

```
truncate table "SysLogs";
```

### 2. 削除後確認用SQL

##### SQL

```
select top 1000 * from "SysLogs";
```
