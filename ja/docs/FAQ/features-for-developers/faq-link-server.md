---
title: プリザンターから外部DBのテーブルを参照したい
category: FAQ：開発者向け機能
order: '0'
status: ''
parts: ''
urlstring: faq-link-server
translationKey: faq-link-server
shortname: 外部DBのテーブルを参照
created: 2021-09-27
updated: 2024-04-29
---

## 回答

データベースがSQLServerの場合は「リンクサーバー」機能、PostgreSQLの場合は「FDW」機能であらかじめ別DBにアクセスできる状態にしたうえで、[拡張SQL](../../developers-guide/extended-features/extended-sql/index.md)を使用します。

---

## 概要

[拡張SQL](../../developers-guide/extended-features/extended-sql/index.md)の「OnSelectingColumn」を使用しプリザンターから外部DBのテーブルを参照するサンプルコードです。参照したい外部DBをSQL Serverの「リンクサーバー」機能を使って参照します。

## 前提条件

1. 事前にリンクサーバの設定が完了している必要があります。
    SQL Serverの場合はリンクサーバ機能を利用します。PostgreSQLの場合は「FDW」機能を利用します。  
    [リンク サーバー \(データベース エンジン\) \- SQL Server \| Microsoft Learn](https://learn.microsoft.com/ja-jp/sql/relational-databases/linked-servers/linked-servers-database-engine?view=sql-server-ver16)  
    [F\.33\. postgres\_fdw](https://www.postgresql.jp/docs/9.6/postgres-fdw.html)  

## 説明

プリザンターから参照する外部DBのテーブル例です。

| id  | 氏名      | 年齢 |
| :-: | :-:       | :-:  |
| 1   | ユーザー1 | 21   |

1. プリザンターのテーブルの分類Aに外部DBテーブルの id が格納されていることとします。
1. 外部DBテーブルの 年齢 をプリザンターの 分類Z に表示します。

## 操作手順

### テーブルの設定

1. プリザンターを開き、テーブルを作成してください。
1. [テーブルの管理](../../managers-guide/manage-table/index.md)を開き[一覧](../../managers-guide/manage-table/grid/index.md)タブと[エディタ](../../users-guide/table/record-authoring/edit-records/table-editor.md)タブで「分類Z」を有効化してください。
1. 対象となるテーブルのサイトIDをメモしてください。

### 拡張SQLの設定

1. 後述のJSONファイル例を LinkSever.json として保存してください
  - 保存先は以下の通りです。
  - C:\web\pleasanter\Implem.Pleasanter\App_Data\Parameters\ExtendedSqls\LinkServer.json

1. SiteIdList をメモしたサイトIDに変更してください。
1. CommandText のSQLのFROM句: [リンクサーバー名].[DB名].[スキーマ名].[テーブル名] [照合順序]は設定したいリンクサーバーと、参照したいテーブル名に変更してください。
1. プリザンターを再起動してください。

## サンプルコード

本サンプルコードはSQLSever用です。

##### JSON(LinkServer.json)

```
{
    "Name": "LinkServerTest",
    "Description": "LinkServerTest",
    "SiteIdList": [xxx],
    "ColumnList": ["ClassZ"],
    "OnSelectingColumn": true,
    "CommandText": "(select age from [LINKSERVER].[postgres].[public].[staff] where id = Results.ClassA COLLATE Japanese_CI_AS)"
}
```

## 関連情報

-   [開発者ガイド：拡張機能：拡張SQL](../../developers-guide/extended-features/extended-sql/index.md)
-   [リンク サーバー \(データベース エンジン\) \- SQL Server \| Microsoft Learn](https://learn.microsoft.com/ja-jp/sql/relational-databases/linked-servers/linked-servers-database-engine?view=sql-server-ver16)
-   [F\.33\. postgres\_fdw](https://www.postgresql.jp/docs/9.6/postgres-fdw.html)
-   [テーブルの管理](../../managers-guide/manage-table/index.md)
-   [テーブルの管理：一覧画面](../../managers-guide/manage-table/grid/index.md)
-   [テーブル機能：レコードのエディタ画面](../../users-guide/table/record-authoring/edit-records/table-editor.md)