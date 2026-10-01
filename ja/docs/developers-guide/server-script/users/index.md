---
title: users
icon: material/alpha-o-box
category: サーバスクリプト
order: '25000'
status: ''
parts: ''
urlstring: server-script-users
translationKey: server-script-users
shortname: users
created: 2021-06-14
updated: 2026-09-08
---

## 概要

[サーバスクリプト](../index.md)で使用可能な「usersオブジェクト」の操作を行うオブジェクトです。

## メソッド

|No|Name|Description|
|:---|:---|:---|
|1|[Create](server-script-users-create.md)|「[サーバスクリプト](../index.md)」で新しい「[ユーザ](../../../managers-guide/user-administration/index.md)」を作成します。|
|2|[Get](server-script-users-get.md)|「userオブジェクト」を取得します。|
|3|[GetList](server-script-users-get-list.md)|絞り込み条件・並び順・ページングを指定して複数のユーザ情報を取得します。|
|4|[Update](server-script-users-update.md)|「サーバスクリプト」で指定したユーザを更新します。|

## 使用例

下記の例では「usersオブジェクト」からユーザID 1 の「userオブジェクト」を取得し,ユーザの名前と組織IDをログに出力します。

##### JavaScript

```
let user = users.Get(1);
context.Log(`${user.Name},${user.DeptId}`);
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)