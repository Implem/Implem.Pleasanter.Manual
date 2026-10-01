---
title: $p.apiUsersGet
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-users-get
translationKey: script-api-users-get
shortname: ''
created: 2020-01-21
updated: 2026-09-08
---

## 概要

AjaxのPOSTリクエストによる値の取得が可能なメソッドに関する説明をします。ユーザの情報などを取得したいときに使用してください。

## 事前準備

APIの操作を行う前に[APIキーの作成](../../api/basics/api-key.md)を実施してください。

## 構文

##### JavaScript

```
$p.apiUsersGet({
    id: <ユーザID>,
    done: <任意の処理>,
    fail: <任意の処理>,
    always: <任意の処理>
});
``` 

## 各パラメータの説明

|パラメータ名|説明|
|:--|:--|
|ユーザID|情報を取得したいユーザID|
|任意の処理|API通信成功(done:必須)、失敗時(fail:任意)、完了時(always：任意)の処理|

## 使用例

##### JavaScript

```
$p.apiUsersGet({
    id: 123,
    done: function (data) {
        console.log(data);
        console.log('ユーザ情報の取得に成功しました。');
    },
    fail: function () {
        console.log('ユーザ情報の取得に失敗しました。');
    },
    always: function () {
        console.log('ユーザ情報の取得が完了しました。');
    }
});
``` 