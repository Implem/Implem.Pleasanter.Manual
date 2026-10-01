---
title: group
icon: material/alpha-o-box
category: サーバスクリプト
order: '31000'
status: ''
parts: ''
urlstring: server-script-group
translationKey: server-script-group
shortname: group
created: 2021-06-08
updated: 2026-09-08
---

## 概要

[サーバスクリプト](../index.md)で[グループ](../../../managers-guide/group-administration/index.md)の情報を読み取るためのオブジェクトです。「groupsオブジェクト」のGetメソッドで取得します。

## プロパティ

|No|プロパティ名|get|set|type|説明|
|:----|:----|:----|:----|:----|:----|
|1|GroupId|○| |int|グループID|
|2|GroupName|○| |string|グループ名|
|3|Body|○| |string|内容|
|4|Disabled|○| |bool|無効|

## メソッド

|No|Name|Description|
|:---|:---|:---|
|1|[ContainsChild](server-script-group-contains-child.md)|[グループ](../../../managers-guide/group-administration/index.md)内に[子グループ](../../../users-guide/hands-on/basics/basic-operations-group-child.md)を含む場合、trueを返します。|
|2|[ContainsDept](server-script-group-contains-dept.md)|[グループ](../../../managers-guide/group-administration/index.md)内に[組織](../../../managers-guide/department-administration/index.md)を含む場合、trueを返します。|
|3|[ContainsUser](server-script-group-contains-user.md)|[グループ](../../../managers-guide/group-administration/index.md)内に[ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)を含む場合、trueを返します。|
|4|[GetChildren](server-script-group-children.md)|[グループ](../../../managers-guide/group-administration/index.md)内の[子グループ](../../../users-guide/hands-on/basics/basic-operations-group-child.md)の「groupオブジェクト」を取得します。|
|5|[GetMembers](server-script-group-get-members.md)|[グループ](../../../managers-guide/group-administration/index.md)内の「groupMemberオブジェクト」を取得します。|

## 使用例

下記の例では「groupsオブジェクト」からグループID 1 の「groupオブジェクト」を取得し「グループメンバー」を列挙しながらメンバーの組織IDとユーザIDをログに出力しています。

##### JavaScript

```
let group = groups.Get(307);
for (let member of group.GetMembers()) {
    context.Log(`${member.DeptId},${member.UserId}`);
}
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [グループ管理機能](../../../managers-guide/group-administration/index.md)
-   [開発者ガイド：サーバスクリプト：group.GetMembers](server-script-group-get-members.md)
-   [開発者ガイド：サーバスクリプト：group.GetChildren](server-script-group-children.md)
-   [子グループ追加](../../../users-guide/hands-on/basics/basic-operations-group-child.md)
-   [開発者ガイド：サーバスクリプト：group.ContainsDept](server-script-group-contains-dept.md)
-   [組織管理機能](../../../managers-guide/department-administration/index.md)
-   [開発者ガイド：サーバスクリプト：group.ContainsUser](server-script-group-contains-user.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)
-   [開発者ガイド：サーバスクリプト：group.ContainsChild](server-script-group-contains-child.md)