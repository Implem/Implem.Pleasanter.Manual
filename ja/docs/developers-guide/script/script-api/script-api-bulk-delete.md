---
title: $p.apiBulkDelete
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-bulk-delete
translationKey: script-api-bulk-delete
shortname: ''
created: 2024-11-12
updated: 2026-07-27
---

## 概要

AjaxのPOSTリクエストにより、レコードを一括削除します。

## 構文

##### JavaScript

```
$p.apiBulkDelete({
    id: <サイトID>,
    data: {
        <データ>
    },
    async: <非同期処理の有無>,
    done: <API通信成功時の処理>,
    fail: <API通信失敗時の処理>,
    always: <API通信完了時の処理>
});
``` 

## パラメータ

|パラメータ名|型|必須|概要|
|:--|:--|:--|:--|
|サイトID|long|○|削除対象レコードが登録されているテーブルのサイトID。|
|データ|object|○|一括削除するレコードの条件等をJSON形式で指定。JSONの仕様は [レコード一括削除API](../../api/table-operations/api-table-bulk-delete.md) の「設定値」を参照。また、本スクリプトの独自仕様としてGridCheckも指定が可能。|
|非同期処理の有無|bool||falseを指定すると同期処理として実行。省略時はtrue（非同期処理）となる。|
|API通信成功時の処理|function|○|API通信成功時に実行する処理。|
|API通信失敗時の処理|function||API通信失敗時に実行する処理。|
|API通信完了時の処理|function||API通信完了時に実行する処理。|

## <データ>にGridCheckを指定した場合

一覧画面でチェックしたレコードを削除します。詳細は使用例4および使用例5を参照。

## 使用例

### 1. 項目の条件で絞ってレコードを削除する場合

##### JavaScript

```
$p.apiBulkDelete({
    id: 123,
    data: {
        View: {
            ColumnFilterHash: {
                Status: "[100,910]"
            }
        }
    },
    done: function (data) {
        console.log(data);
    },
    fail: function (data) {
        console.log(data);
    },
    always: function (data) {
        console.log(data);
    }
});
```

### 2. 指定した複数レコードを削除する場合（レコードIDが135,376のレコードを削除）

##### JavaScript

```
$p.apiBulkDelete({
    id: 123,
    data: {
        Selected: [
            135,
            376
        ]
    },
    done: function (data) {
        console.log(data);
    },
    fail: function (data) {
        console.log(data);
    },
    always: function (data) {
        console.log(data);
    }
});
```

### 3. 対象テーブルの全レコードを削除する場合

##### JavaScript

```
$p.apiBulkDelete({
    id: 123,
    data: {
        All: true
    },
    done: function (data) {
        console.log(data);
    },
    fail: function (data) {
        console.log(data);
    },
    always: function (data) {
        console.log(data);
    }
});
```

### 4. 一覧画面でチェックしたレコードを削除する場合

##### JavaScript

```
$p.apiBulkDelete({
    id: 123,
    data: {
        GridCheck: true
    },
    done: function (data) {
        console.log(data);
    },
    fail: function (data) {
        console.log(data);
    },
    always: function (data) {
        console.log(data);
    }
});
```

### 5. 一覧画面でチェックしたレコードを物理削除する場合

##### JavaScript

```
$p.apiBulkDelete({
    id: 123,
    data: {
        GridCheck: true,
        PhysicalDelete: true
    },
    done: function (data) {
        console.log(data);
    },
    fail: function (data) {
        console.log(data);
    },
    always: function (data) {
        console.log(data);
    }
});
```
