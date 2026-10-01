---
title: group.GetMembers
icon: material/alpha-m-box
category: サーバスクリプト
order: '31100'
status: ''
parts: ''
urlstring: server-script-group-get-members
translationKey: server-script-group-get-members
shortname: group.GetMembers
created: 2021-06-09
updated: 2026-09-08
---

## 概要

[サーバスクリプト](../index.md)で「groupオブジェクト」から「groupMemberオブジェクト」のコレクションを取得します。

## 構文

```js
group.GetMembers()
```

## 戻り値

「groupMemberオブジェクト」のコレクションを返却します。

## 使用例

下記の例ではグループID 1 のグループに所属するメンバーの組織IDとユーザIDをログに出力します。

##### JavaScript

```js
let group = groups.Get(1);
for (let member of group.GetMembers()) {
    context.Log(`${member.DeptId},${member.UserId}`);
}
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)