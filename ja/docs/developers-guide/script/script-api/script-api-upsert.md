---
title: $p.apiUpsert
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-upsert
translationKey: script-api-upsert
shortname: ''
created: 2024-04-12
updated: 2026-08-18
---

## 概要

AjaxのPOSTリクエストにより、レコードおよびWikiを作成・更新します。

-   指定したキー項目に一致するレコードがある場合：該当レコードを更新
-   指定したキー項目の値がNULLの場合：レコードを新規作成
-   一致するレコードがない場合：レコードを新規作成

## 使い方

##### JavaScript

```
$p.apiUpsert({
    id: <サイトID>,
    data: {
        <データ>
    },
    done: <任意の処理>,
    fail: <任意の処理>,
    always: <任意の処理>
});
``` 

## 各パラメータの説明

|パラメータ名|説明|
|:--|:--|
|サイトID|任意のサイトID|
|データ|POSTするjsonデータ|
|任意の処理|API通信成功(done:必須)、失敗時(fail:任意)、完了時(always：任意)の処理|  

## 記述方法

##### JavaScript

```
$p.apiUpsert({
    id: 123,
    data: {
        ApiVersion: 1.1,
        Keys: [
            'ClassA',
            'ClassB'
        ],
        ClassHash: {
            ClassA: 'テストデータ',
            ClassB: 'テストデータ詳細です'
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
