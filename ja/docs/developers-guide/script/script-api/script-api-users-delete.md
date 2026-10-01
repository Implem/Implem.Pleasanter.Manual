---
title: $p.apiUsersDelete
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-users-delete
translationKey: script-api-users-delete
shortname: ''
created: 2020-01-21
updated: 2026-09-08
---

## 概要

AjaxのPOSTリクエストにより、ユーザを削除します。

## 構文

##### JavaScript

```
$p.apiUsersDelete({
    id: <ユーザID>,
    done: <任意の処理>,
    fail: <任意の処理>,
    always: <任意の処理>
});
```

## 各パラメータの説明

|パラメータ名|説明|
|:--|:--|
|ユーザID|ユーザのID情報|
|任意の処理|API通信成功(done:必須)、失敗時(fail:任意)、完了時(always：任意)の処理|

## 使用例

##### JavaScript

```
$p.apiUsersDelete({
    id: 123,
    done: function (data) {
        console.log(data);
        console.log('ユーザ情報の削除に成功しました。');
    },
    fail: function () {
        console.log('ユーザ情報の削除に失敗しました。');
    },
    always: function () {
        console.log('ユーザ情報の削除が完了しました。');
    }
});
```
