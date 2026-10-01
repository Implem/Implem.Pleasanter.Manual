---
title: groups.Update
icon: material/alpha-m-box
category: サーバスクリプト
order: '31400'
status: ''
parts: ''
urlstring: server-script-groups-update
translationKey: server-script-groups-update
shortname: groups.Update
created: 2023-03-28
updated: 2026-09-08
---

## 概要

[サーバスクリプト](../index.md)で指定したグループIDの[グループ](../../../managers-guide/group-administration/index.md)を更新します。

## 前提条件

本機能によるグループの更新にはサイトの管理者権限が必要です。サイトの管理者権限がないユーザで更新したい場合、サイトの管理権限をもったユーザのAPIキーの指定が必要です。

## 構文

```
groups.Update(groupId, data)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|groupId|object|○|対象グループのグループIDを指定|
|data|string|○|更新内容をJSON形式で指定|

## 戻り値

指定した[グループ](../../../managers-guide/group-administration/index.md)が更新できた場合には true、更新できなかった場合には false を返却します。

## 使用例

下記の例では、グループ 100 の[グループ](../../../managers-guide/group-administration/index.md)のメンバーをユーザID 5 の[ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)、組織ID 3 の[組織](../../../managers-guide/department-administration/index.md)で更新します。メンバーがユーザの場合は "User,ユーザID,管理者権限(true/false)"、組織の場合は "Dept,組織ID,管理者権限(true/false)" を指定してください。メンバーの更新は指定したもので全て洗い替えとなります。

##### JavaScript

```
const apiKey = 'xxxxx...';
const userId = 5;
const deptId = 3;
const groupId = 100;
let groupMembers = [
    `User,${userId},true`,
    `Dept,${deptId},false`
];
const data = {
    ApiKey: apiKey,
    GroupMembers: groupMembers
};
groups.Update(groupId, JSON.stringify(data));
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [グループ管理機能](../../../managers-guide/group-administration/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)
-   [組織管理機能](../../../managers-guide/department-administration/index.md)