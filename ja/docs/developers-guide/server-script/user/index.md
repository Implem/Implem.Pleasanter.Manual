---
title: user
icon: material/alpha-o-box
category: サーバスクリプト
order: '25100'
status: ''
parts: ''
urlstring: server-script-user
translationKey: server-script-user
shortname: user
created: 2021-06-14
updated: 2026-08-14
---

## 概要

[サーバスクリプト](../index.md)で[ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)の情報を読み取るためのオブジェクトです。「usersオブジェクト」のGetメソッドで取得します。

## プロパティ

|No|プロパティ名|get|set|type|説明|
|:----|:----|:----|:----|:----|:----|
|1|TenantId|○| |int|テナントID|
|2|UserId|○| |int|ユーザID|
|3|DeptId|○| |int|組織ID|
|4|LoginId|○| |string|ログインID|
|5|Name|○| |string|名前|
|6|UserCode|○| |string|ユーザコード|
|7|TenantManager|○| |bool|テナント管理者|
|8|Disabled|○| |bool|無効|

## 使用例

下記の例では「usersオブジェクト」からユーザID 1 の「userオブジェクト」を取得し,ユーザの名前と組織IDをログに出力します。

##### JavaScript

```
let user = users.Get(1);
context.Log(`${user.Name},${user.DeptId}`);
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)