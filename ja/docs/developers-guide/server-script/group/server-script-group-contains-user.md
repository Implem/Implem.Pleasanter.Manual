---
title: group.ContainsUser
icon: material/alpha-m-box
category: サーバスクリプト
order: '31300'
status: ''
parts: ''
urlstring: server-script-group-contains-user
translationKey: server-script-group-contains-user
shortname: group.ContainsUser
created: 2021-06-09
updated: 2026-07-08
---

## 概要

[サーバスクリプト](../index.md)で「groupオブジェクト」に指定した[ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)または[ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)の所属する[組織](../../../managers-guide/department-administration/index.md)が含まれるか判定します。

## 構文

```
group.ContainsUser(userId)
```

## 戻り値

指定した[ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)が含まれる場合には true 含まれない場合には false を返却します。指定した[ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)の所属する[組織](../../../managers-guide/department-administration/index.md)が含まれる場合にも true を返却します。

## 使用例

下記の例ではグループID 1 の[グループ](../../../managers-guide/group-administration/index.md)にログインユーザまたはログインユーザの所属する[組織](../../../managers-guide/department-administration/index.md)が含まれるか判定します。

##### JavaScript

```
let group = groups.Get(1);
if (group.ContainsUser(context.UserId)) {
    context.Log('contains');
} else {
    context.Log('not contains');
}
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)
-   [組織管理機能](../../../managers-guide/department-administration/index.md)
-   [グループ管理機能](../../../managers-guide/group-administration/index.md)