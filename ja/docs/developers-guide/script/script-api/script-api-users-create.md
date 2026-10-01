---
title: $p.apiUsersCreate
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-users-create
translationKey: script-api-users-create
shortname: ''
created: 2023-10-02
updated: 2026-09-08
---

## 概要

AjaxのPOSTリクエストにより、ユーザを作成します。

## 構文

##### JavaScript

```
$p.apiUsersCreate({
    data: {
        <作成するユーザ情報>
    },
    done: <任意の処理>,
    fail: <任意の処理>,
    always: <任意の処理>
});
``` 

## 各パラメータの説明

|パラメータ名|説明|必須|
|:--|:--|:--:|
|data|作成するユーザ情報　※欄外補足参照|-|
|done|API通信成功|○|
|fail|API通信失敗|-|
|always|完了時|-|

※作成するユーザ情報は、[APIユーザ作成時](../../api/user-operations/api-user-create.md)と同等のパラメータを設定します。リンク先のマニュアルを参照にパラメータを設定してください。

## 使用例

##### JavaScript

```
$p.apiUsersCreate({
    data: {
        LoginId: 'TESTUSER',
        Name: 'USER1',
        Password: '123456',
        MailAddresses: [
            'test@example.co.jp'
        ],
    },
    done: function (data) {
        console.log(data);
        console.log('ユーザ情報の作成に成功しました。');
    },
    fail: function (data) {
        console.log('ユーザ情報の作成に失敗しました。');
    },
    always: function (data) {
        console.log('ユーザ情報の作成が完了しました。');
    }
});
```
