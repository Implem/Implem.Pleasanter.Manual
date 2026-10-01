---
title: users.Get
icon: material/alpha-m-box
category: サーバスクリプト
order: '25000'
status: ''
parts: ''
urlstring: server-script-users-get
shortname: users.Get
created: 2026-08-25
updated: 2026-09-08
---

## 概要

サーバスクリプトで、ユーザIDを指定して1件のユーザ情報を取得します。ユーザを複数件まとめて取得したい場合は、[users.GetList](server-script-users-get-list.md) を使用してください。

## メソッド

```javascript
users.Get(userId);
```

## パラメータ

| パラメータ | 型 | 必須 | 説明 |
| --- | --- | --- | --- |
| userId | long | ○ | 取得対象のユーザIDを指定します。 |

## 使用例

```javascript
const user = users.Get(11);
if (user) {
    context.Log(user.LoginId + ', ' + user.Name);
} else {
    context.Log('対象のユーザが存在しません。');
}
```

## 戻り値

「userオブジェクト」を返します。オブジェクトのレイアウトは「[開発者ガイド：サーバスクリプト：user](../user/index.md)」を参照してください。指定したIDのユーザが存在しない場合は null を返します。

```json
{
    "TenantId": 1,
    "UserId": 11,
    "DeptId": 3,
    "LoginId": "yamada",
    "Name": "山田太郎",
    "UserCode": "U0011",
    "TenantManager": false,
    "ServiceManager": false,
    "Disabled": false,
    "ClassHash": {
        "ClassA": "test-class-column"
    },
    "NumHash": {
        "NumA": 100
    },
    "DateHash": {
        "DateA": "2026-08-19"
    },
    "DescriptionHash": {
        "DescriptionA": "補足説明"
    },
    "CheckHash": {
        "CheckA": true
    }
}
```

## 注意事項
こちらは「[サーバスクリプト](../index.md)」で使用するメソッドです。「[スクリプト](../../script/index.md)」では使用できません。
