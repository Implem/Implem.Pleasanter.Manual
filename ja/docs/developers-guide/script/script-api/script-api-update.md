---
title: $p.apiUpdate
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-update
translationKey: script-api-update
shortname: ''
created: 2019-08-12
updated: 2026-08-04
---

## 概要

AjaxのPOSTリクエストにより、レコードおよびWikiを更新します。

## 使い方

##### JavaScript

```
$p.apiUpdate({
    id: <レコードID>,
    data: {
        <更新データ>
    },
    done: <任意の処理>,
    fail: <任意の処理>,
    always: <任意の処理>
});
``` 

## 各パラメータの説明

|パラメータ名|説明|
|:--|:--|
|レコードID|操作対象のレコードID
|更新データ|POSTするjsonデータ|
|任意の処理|API通信成功(done:必須)、失敗時(fail:任意)、完了時(always：任意)の処理|  

## 記述方法

##### JavaScript

```
$p.apiUpdate({
    id: 123,
    data: {
        ApiVersion: 1.1,
        ClassHash: {
            ClassA: 'テストデータ'
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
