---
title: $p.apiCreate
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-create
translationKey: script-api-create
shortname: ''
created: 2020-01-09
updated: 2026-08-04
---

## 概要

AjaxのPOSTリクエストにより、新規レコードを作成します。

## 構文

##### JavaScript

```
$p.apiCreate({
    id: (サイトID),
    data: {
        項目名: '(値)'
    },
    done: (任意の処理),
    fail: (任意の処理),
    always: (任意の処理)
});
``` 

## 各パラメータの説明

|パラメータ名|説明|
|:--|:--|
|id|任意のサイトID|
|data|POSTするJSON|
|done|API通信成功時の処理（任意）|
|fail|API通信失敗時の処理（任意）|
|always|API通信完了時の処理（任意）|   

## 使用例

以下のサンプルコードは、サイトID:123のテーブルにタイトルが"コーヒー"、分類Aが"ブラック" のレコードを作成します。

##### JavaScript

```
$p.apiCreate({
    id: 123,
    data: {
        Title: 'コーヒー',
        ClassHash: {
            ClassA: 'ブラック'
        }
    },
    done: function (data) {
        $p.clearMessage();
        const message = {
            Css: 'alert-success',
            Text: '新規レコードを作成しました'
        };
        $p.setMessage('#Message',JSON.stringify(message));
    },
    fail: function (data) {
        console.log(data);
    }
});
```
