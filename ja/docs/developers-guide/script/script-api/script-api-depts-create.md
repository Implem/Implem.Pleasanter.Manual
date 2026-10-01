---
title: '$p.apiDeptsCreate'
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-depts-create
translationKey: script-api-depts-create
shortname: $p.apiDeptsCreate
created: 2026-07-22
updated: 2026-09-08
---

## 概要

AjaxのPOSTリクエストにより、組織を作成します。

## 構文

##### JavaScript

```javascript
$p.apiDeptsCreate({
    payload: {
        <作成する組織情報>
    },
    done: <API通信成功時の処理>,
    fail: <API通信失敗時の処理>,
    always: <API通信完了時の処理>
});
```

## パラメータ

|パラメータ名|型|必須|概要|
|:--|:--|:--|:--|
|作成する組織情報|object||作成する組織情報をJSON形式で指定。|
|API通信成功時の処理|function|○|API通信成功時に実行する処理。|
|API通信失敗時の処理|function||API通信失敗時に実行する処理。|
|API通信完了時の処理|function||API通信完了時に実行する処理。|

## 使用例

##### JavaScript

```javascript
$p.apiDeptsCreate({
    payload: {
        DeptCode: "[登録する組織の組織コード]",
        DeptName: "[登録する組織の名前]",
        Body: "[登録する組織の説明]",
        ClassHash: {
            ClassA: "test-class-column"
        }
    },
    done: function (data) {
        console.log(data);
        console.log('組織情報の作成に成功しました。');
    },
    fail: function (data) {
        console.log('組織情報の作成に失敗しました。');
    },
    always: function (data) {
        console.log('組織情報の作成が完了しました。');
    }
});
```

### ClassHash

「[拡張項目](../../extended-features/extended-column.md)」に値を設定する場合は、カラム名をパラメータとして指定します。

##### JavaScript

```javascript
ClassHash: {
    ClassA: "test-class-column"
}
```

## 戻り値

正常終了時は以下のようなオブジェクトが返却されます。

##### JavaScript

```json
{
    "Id": 96,
    "StatusCode": 200,
    "Message": "\" [登録する組織の名前] \" を作成しました。"
}
```

## 戻り値の項目

| 項目       | 説明                       |
| ---------- | -------------------------- |
| Id         | 作成された組織のID         |
| StatusCode | 実行結果のステータスコード |
| Message    | 実行結果メッセージ         |

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.5.8.0 以降|機能追加|
