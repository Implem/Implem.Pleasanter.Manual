---
title: '$p.apiDeptsUpdate'
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-depts-update
shortname: $p.apiDeptsUpdate
created: 2026-08-24
updated: 2026-09-08
---

## 概要

AjaxのPOSTリクエストにより、組織を更新します。

## 構文

##### JavaScript

```javascript
$p.apiDeptsUpdate({
    id: <更新する組織のID>,
    data: {
        <更新する組織情報>
    },
    done: <任意の処理>,
    fail: <任意の処理>,
    always: <任意の処理>
});
```

## パラメータ

| パラメータ名 | 型 | 必須 | 概要 |
| --- | --- | --- | --- |
| id | long | ○ | 更新する組織のID |
| data | object |  | 更新する組織情報をJSON形式で指定 ※欄外補足参照 |
|done|function|○|API通信成功時に実行する処理|
|fail|function||API通信失敗時に実行する処理|
|always|function||API通信完了時に実行する処理|

※更新する組織情報は、[API組織更新](../../api/department-operations/api-dept-update.md)と同等のパラメータを設定します。リンク先のマニュアルを参照してパラメータを設定してください。

## 使用例

```javascript
$p.apiDeptsUpdate({
    id: 2,
    data: {
        DeptName: '[更新後の組織名]',
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
    },
    done: function (data) {
        console.log(data);
        console.log('組織情報の更新に成功しました。');
    },
    fail: function (data) {
        console.log('組織情報の更新に失敗しました。');
    },
    always: function (data) {
        console.log('組織情報の更新が完了しました。');
    }
});
```

## 戻り値

正常終了時は以下のようなオブジェクトが返却されます。

```json
{
    "Id": 2,
    "StatusCode": 200,
    "Message": "\" [更新後の組織名] \" を更新しました。"
}
```

## 戻り値の項目

| 項目 | 説明 |
| --- | --- |
| Id | 更新された組織のID |
| StatusCode | 実行結果のステータスコード |
| Message | 実行結果メッセージ |

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.5.8.0 以降|機能追加|

## 関連情報

[$p.apiDeptsGet](script-api-depts-get.md)
[開発者ガイド：スクリプト：$p.apiDeptsCreate](script-api-depts-create.md)
[開発者ガイド：スクリプト：$p.apiDeptsDelete](script-api-depts-delete.md)
[開発者ガイド：JSONデータレイアウト：Dept](../../json-data-layout/api-dept.md)
