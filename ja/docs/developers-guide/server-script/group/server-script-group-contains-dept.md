---
title: group.ContainsDept
icon: material/alpha-m-box
category: サーバスクリプト
order: '31200'
status: ''
parts: ''
urlstring: server-script-group-contains-dept
translationKey: server-script-group-contains-dept
shortname: group.ContainsDept
created: 2021-06-09
updated: 2023-07-05
---

## 概要

[サーバスクリプト](../index.md)で「groupオブジェクト」に指定した[組織](../../../managers-guide/department-administration/index.md)が含まれるか判定します。

## 構文

```
group.ContainsDept(deptId)
```

## 戻り値

指定した[組織](../../../managers-guide/department-administration/index.md)が含まれる場合には true 含まれない場合には false を返却します。

## 使用例

下記の例ではグループID 1 の[グループ](../../../managers-guide/group-administration/index.md)にログインユーザの[組織](../../../managers-guide/department-administration/index.md)が含まれるか判定します。

##### JavaScript

```
let group = groups.Get(1);
if (group.ContainsDept(context.DeptId)) {
    context.Log('contains');
} else {
    context.Log('not contains');
}
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [組織管理機能](../../../managers-guide/department-administration/index.md)
-   [グループ管理機能](../../../managers-guide/group-administration/index.md)