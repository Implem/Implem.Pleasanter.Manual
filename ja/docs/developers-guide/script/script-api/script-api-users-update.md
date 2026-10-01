---
title: $p.apiUsersUpdate
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-users-update
translationKey: script-api-users-update
shortname: ''
created: 2020-01-21
updated: 2026-09-08
---

## 概要

AjaxのPOSTリクエストにより、ユーザを更新します。

## 構文

##### JavaScript

```
$p.apiUsersUpdate({
    id: <ユーザID>,
    data: {
        <更新データ>
    },
    done: <任意の処理>,
    fail: <任意の処理>,
    always: <任意の処理>
});
```   

※ Password、ApiKeyは変更できません。

## 各キーの説明

|キー名称|説明|必須|
|:--|:--|:--:|
|id|更新するユーザのID情報|○|
|data|指定ユーザ情報の更新情報|○|
|done|API通信成功|○|
|fail|API通信失敗|-|
|always|完了時|-|

## 使用例

##### JavaScript

```
$p.apiUsersUpdate({
    id: 123,
    data: {
        LoginId: 'HAYATO',
        Name: '中野 隼人'
    },
    done: function(data){
        console.log(data);
    },
    fail: function(data){
        console.log(data);
    }
});
```
