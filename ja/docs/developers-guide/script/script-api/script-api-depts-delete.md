---
title: '$p.apiDeptsDelete'
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-depts-delete
shortname: $p.apiDeptsDelete
created: 2026-08-24
updated: 2026-09-08
---

## 概要
AjaxのPOSTリクエストにより、組織を削除します。

## 構文

```javascript
$p.apiDeptsDelete({
    id: <削除する組織のID>,
    done: <任意の処理>,
    fail: <任意の処理>,
    always: <任意の処理>
});
```

## パラメータ

|パラメータ名|型|必須|概要|
|:--|:--|:--|:--|
|id|long|○|削除する組織のID|
|done|function|○|API通信成功時の処理|
|fail|function||API通信失敗時の処理|
|always|function||API通信完了時の処理|   

## 使用例

```javascript
$p.apiDeptsDelete({
    id: 2,
    done: function (data) {
        console.log(data);
        console.log('組織情報の削除に成功しました。');
    },
    fail: function (data) {
        console.log('組織情報の削除に失敗しました。');
    },
    always: function (data) {
        console.log('組織情報の削除が完了しました。');
    }
});
```

## 戻り値

正常終了時は以下のようなオブジェクトが返却されます。

```json
{
    "Id": 2,
    "StatusCode": 200,
    "Message": "\" [削除した組織の名前] \" を削除しました。"
}
```

## 戻り値の項目

| 項目 | 説明 |
| --- | --- |
| Id | 削除された組織のID |
| StatusCode | 実行結果のステータスコード |
| Message | 実行結果メッセージ |

## 補足

- 対象IDの組織が存在しない場合は404（Not Found）エラーが返却されます。
- 削除できない状態（参照制約など）の場合は403（Forbidden）エラーが返却されます。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.5.8.0 以降|機能追加|

## 関連情報

[$p.apiDeptsGet](script-api-depts-get.md)
[開発者ガイド：スクリプト：$p.apiDeptsCreate](script-api-depts-create.md)
[開発者ガイド：スクリプト：$p.apiDeptsUpdate](script-api-depts-update.md)
