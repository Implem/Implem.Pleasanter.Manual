---
title: $p.apiDeptsGet
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-depts-get
translationKey: script-api-depts-get
shortname: ''
created: 2024-11-12
updated: 2026-09-08
---

## 概要

AjaxのPOSTリクエストにより、組織情報を取得します。

## 事前準備

APIの操作を行う前に[APIキーの作成](../../api/basics/api-key.md)を実施してください。

## 構文

##### JavaScript

```
$p.apiDeptsGet({
    id: <組織ID>,
    done: <任意の処理>,
    fail: <任意の処理>,
    always: <任意の処理>
});
``` 

## 各パラメータの説明

|パラメータ名|説明|
|:--|:--|
|組織ID|情報を取得したい組織ID|
|任意の処理|API通信成功(done:必須)、失敗時(fail:任意)、完了時(always：任意)の処理|

## 使用例

##### JavaScript

```
$p.apiDeptsGet({
    id: 123,
    done: function (data) {
        console.log(data);
        console.log('組織情報の取得に成功しました。');
    },
    fail: function () {
        console.log('組織情報の取得に失敗しました。');
    },
    always: function () {
        console.log('組織情報の取得が完了しました。');
    }
});
``` 
