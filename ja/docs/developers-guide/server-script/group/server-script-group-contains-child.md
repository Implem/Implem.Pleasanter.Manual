---
title: group.ContainsChild
icon: material/alpha-m-box
category: サーバスクリプト
order: '31200'
status: ''
parts: ''
urlstring: server-script-group-contains-child
translationKey: server-script-group-contains-child
shortname: group.ContainsChild
created: 2024-05-07
updated: 2024-05-14
---

## 概要

[サーバスクリプト](../index.md)で「groupオブジェクト」に指定した[子グループ](../../../users-guide/hands-on/basics/basic-operations-group-child.md)が含まれるか判定します。

## 構文

```
group.ContainsChild(groupId)
```

## 戻り値

指定した[子グループ](../../../users-guide/hands-on/basics/basic-operations-group-child.md)が含まれる場合には true 含まれない場合には false を返却します。

## 使用例

下記の例ではグループID 1 の[グループ](../../../managers-guide/group-administration/index.md)にグループID 2 の[子グループ](../../../users-guide/hands-on/basics/basic-operations-group-child.md)が含まれるか判定します。

##### JavaScript

```
let group = groups.Get(1);
if (group.ContainsChild(2)) {
    context.Log('contains');
} else {
    context.Log('not contains');
}
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [子グループ追加](../../../users-guide/hands-on/basics/basic-operations-group-child.md)
-   [グループ管理機能](../../../managers-guide/group-administration/index.md)