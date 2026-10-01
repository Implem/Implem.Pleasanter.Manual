---
title: Webサーバとデータベースサーバを別々のサーバに分けて構築したい
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-separate-web-and-db
translationKey: faq-separate-web-and-db
shortname: ''
created: 2019-10-09
updated: 2024-04-29
---

## 回答

パラメータ[Rds.json](../../setup/parameters/rds-json.md)の接続文字列のServerキーワードにデータベースサーバのIPアドレスまたはホスト名を設定してください。

---

## 概要

Webサーバとデータベースサーバを別々のサーバに分けて構築するための設定方法です。このFAQではWindows/SQL Serverを例に記載しておりますが、Linux/PostgreSQL環境でも同様の方法で構築可能です。

## 構成例

### サーバA：Webサーバ

-   IIS
-   プリザンター

### サーバB：データベースサーバ

-   SQL Server 2019 Express with Advanced Services

## 設定方法

「プリザンターをWindowsにインストールする」手順の[Rds.json](../../setup/parameters/rds-json.md)を編集する際に、サーバB：データベースサーバに接続するための接続文字列を設定してください。

## 設定例（サーバBが 192.168.1.10 の場合）

```json title="Rds.json" linenums="1" hl_lines="4-6"
{
    "Dbms": "SQLServer",
    "Provider": "Local",
    "SaConnectionString": "Server=192.168.1.10;Database=master;UID=sa;PWD=SetSaPWD;Connection Timeout=30;",
    "OwnerConnectionString": "Server=192.168.1.10;Database=#ServiceName#;UID=#ServiceName#_Owner;PWD=SetAdminsPWD;Connection Timeout=30;",
    "UserConnectionString": "Server=192.168.1.10;Database=#ServiceName#;UID=#ServiceName#_User;PWD=SetUsersPWD;Connection Timeout=30;",
    "SqlCommandTimeOut": 0,
    "MinimumTime": 3,
    "DeadlockRetryCount": 4,
    "DeadlockRetryInterval": 1000,
    "DisableIndexChangeDetection": true
}
```

## 関連情報

-   [パラメータ設定：Rds.json](../../setup/parameters/rds-json.md)
