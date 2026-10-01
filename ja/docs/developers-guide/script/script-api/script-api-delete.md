---
title: $p.apiDelete
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-delete
translationKey: script-api-delete
shortname: ''
created: 2019-08-12
updated: 2026-07-22
---

## 概要

AjaxのPOSTリクエストにより、レコードおよびWikiを削除します。

## 使い方

##### JavaScript

```
$p.apiDelete({
    id: <レコードID>,
    done: <任意の処理>,
    fail: <任意の処理>,
    always: <任意の処理>
});
``` 

## 各パラメータの説明

|パラメータ名|説明|
|:--|:--|
|レコードID|操作対象のレコードID|
|任意の処理|API通信成功(done:必須)、失敗時(fail:任意)、完了時(always：任意)の処理|  

## 記述方法

##### JavaScript

```
$p.apiDelete({
    id: 123,
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

## サンプルコード

[FAQ:サンプルコード：ステータスが完了になったら別レコードを削除させたい](../../../FAQ/editor/faq-delete-complete-record.md)
