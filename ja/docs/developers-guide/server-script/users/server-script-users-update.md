---
title: users.Update
icon: material/alpha-m-box
category: サーバスクリプト
order: '25000'
status: ''
parts: ''
urlstring: server-script-users-update
shortname: users.Update
created: 2026-08-25
updated: 2026-09-08
---

## 概要

サーバスクリプトで指定したユーザを更新します。

## メソッド

```javascript
users.Update(userId, user);
```

## パラメータ

| パラメータ | 型 | 必須 | 説明 |
| --- | --- | --- | --- |
| userId | long | ○ | 更新対象のユーザIDを指定します。 |
| user | string | ○ | 更新するユーザ情報をJSON形式の文字列で指定します。指定内容は「[JSONデータレイアウト：User](../../json-data-layout/api-user.md)」を参照してください。 |

## 使用例

下記の例ではユーザID 11 の氏名、組織、拡張項目を更新します。

```javascript
const userId = 11;

const data = {
    Name: '田中太郎',
    DeptId: 3,
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

users.Update(userId, JSON.stringify(data));
```

## 戻り値

ユーザの更新に成功した場合は true、失敗した場合は false を返します。

## 注意事項
こちらは「[サーバスクリプト](../index.md)」で使用するメソッドです。「[スクリプト](../../script/index.md)」では使用できません。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.5.8.0 以降|機能追加|
