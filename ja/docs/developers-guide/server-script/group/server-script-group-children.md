---
title: group.GetChildren
icon: material/alpha-m-box
category: サーバスクリプト
order: '31100'
status: ''
parts: ''
urlstring: server-script-group-children
translationKey: server-script-group-children
shortname: GetChildren
created: 2024-05-07
updated: 2026-09-08
---

## 概要

[サーバスクリプト](../index.md)で「groupオブジェクト」から[子グループ](../../../users-guide/hands-on/basics/basic-operations-group-child.md)一覧の「groupオブジェクト」のコレクションを取得します。

## 構文

```
group.GetChildren()
```

## 戻り値

「groupオブジェクト」のコレクションを返却します。

## 使用例

下記の例ではグループID 1 のグループに所属する子グループのグループIDをログに出力します。

##### JavaScript

```
let group = groups.Get(1);
for (let member of group.GetChildren()) {
    context.Log(`${member.GroupId}`);
}
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [子グループ追加](../../../users-guide/hands-on/basics/basic-operations-group-child.md)