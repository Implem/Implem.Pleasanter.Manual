---
title: プリザンターのグループに所属しているユーザの一覧を取得したい。
category: FAQ：開発者向け機能
order: '0'
status: ''
parts: ''
urlstring: faq-group-members-sql
translationKey: faq-group-members-sql
shortname: ''
created: 2023-01-06
updated: 2024-12-19
---

## 回答

以下方法で取得してください。
1. [グループ取得API](../../developers-guide/api/group-operations/api-group-get.md)を使用
1. スクリプト[$p.apiGroupsGet](../../developers-guide/script/script-api/script-api-groups-get.md)を使用
1. サーバスクリプト[groups.Get](../../developers-guide/server-script/groups/index.md)、「group.GroupMembers」を使用
1. SQLを使用。本ページで説明します。

---

## 概要

プリザンターの[グループ](../../managers-guide/group-administration/index.md)に所属している[ユーザ](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)の一覧を取得するSQL文のサンプルです。

## 手順

SQL Server Management StudioやAzure Data Studio等を使用して、プリザンターのデータベースに接続し、下記のSQLを実行してください。下記のSQLは SQL Server / PostgreSQL 両方に対応しています。

## サンプルコード

```sql
select 
	"Groups"."GroupId"
	,"Groups"."GroupName"
	,"Users"."UserId"
	,"Users"."LoginId"
	,"Users"."Name"
from "Groups" inner join "GroupMembers" on "Groups"."GroupId" = "GroupMembers"."GroupId"
	inner join "Users" on "GroupMembers"."UserId" = "Users"."UserId"
-- union配下を削除すると、組織経由のユーザは取得されません。
union
select 
	"Groups"."GroupId"
	,"Groups"."GroupName"
	,"Users"."UserId"
	,"Users"."LoginId"
	,"Users"."Name"
from "Groups" inner join "GroupMembers" on "Groups"."GroupId" = "GroupMembers"."GroupId"
	inner join "Depts" on "GroupMembers"."DeptId" = "Depts"."DeptId"
	inner join "Users" on "Depts"."DeptId" = "Users"."DeptId"
```

## 実行結果のイメージ

![SQLの実行結果のイメージ。グループに所属するユーザの一覧が並ぶ](https://pleasanter.org/files/images/ja/FAQ/features-for-developers/assets/58db164d23bc462c8e352dcb64730e51.png)

## 関連情報

-   [開発者ガイド：API：グループ操作：グループ取得](../../developers-guide/api/group-operations/api-group-get.md)
-   [$p.apiGroupsGet](../../developers-guide/script/script-api/script-api-groups-get.md)
-   [開発者ガイド：サーバスクリプト：groups](../../developers-guide/server-script/groups/index.md)
-   [グループ管理機能](../../managers-guide/group-administration/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)