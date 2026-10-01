---
title: users.Create
icon: material/alpha-m-box
category: サーバスクリプト
order: '25000'
status: ''
parts: ''
urlstring: server-script-users-create
shortname: users.Create
created: 2026-08-25
updated: 2026-09-08
---

## 概要

「[サーバスクリプト](../index.md)」で新しい「[ユーザ](../../../managers-guide/user-administration/index.md)」を作成します。[users](index.md)オブジェクトのメソッドです。

## メソッド

```javascript
users.Create(user);
```

## パラメータ

| パラメータ | 型 | 必須 | 説明 |
| --- | --- | --- | --- |
| user | string | ○ | 作成するユーザ情報をJSON形式の文字列で指定します。指定内容は「[JSONデータレイアウト：User](../../json-data-layout/api-user.md)」を参照してください。 |

## 使用例

```javascript
const payload = {
    LoginId: 'yamada',
    Password: '[初期パスワード]',
    Name: '山田太郎',
    UserCode: 'U0011',
    DeptId: 3,
    Body: '[登録するユーザの説明]',
    Disabled: false,
    ClassHash: {
        ClassA: 'test-class-column'
    },
    NumHash: {
        NumA: 100
    },
    DateHash: {
        DateA: '2026-08-19'
    },
    DescriptionHash: {
        DescriptionA: '補足説明'
    },
    CheckHash: {
        CheckA: true
    }
};

const createok = users.Create(JSON.stringify(payload));
context.Log(createok);
```

## 戻り値

指定した「[ユーザ](../../../managers-guide/user-administration/index.md)」の作成に成功した場合はtrue、失敗した場合はfalseを返します。 

## 注意事項
こちらは「[サーバスクリプト](../index.md)」で使用するメソッドです。「[スクリプト](../../script/index.md)」では使用できません。
## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.5.8.0 以降|機能追加|
