---
title: $p.apiDeleteSite
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-delete-site
translationKey: script-api-delete-site
shortname: $p.apiDeleteSite
created: 2022-07-05
updated: 2025-10-06
---

## 概要

AjaxのPOSTリクエストにより、サイトを削除します。

## 構文

##### JavaScript

```
$p.apiDeleteSite({
    id: <削除対象サイトID>,
    done: <任意の処理>,
    fail: <任意の処理>,
    always: <任意の処理>
});
``` 

## 各パラメータの説明

|パラメータ名|説明|必須|
|:--|:--|:--:|
|id|削除対象のサイトID|○|
|done|API通信成功|○|
|fail|API通信失敗|-|
|always|完了時|-|

## 使用例

##### JavaScript

```
$p.apiDeleteSite({
    id: 123,
    done: function (data) {
        console.log(data);
        console.log('サイト情報の削除に成功しました。');
    },
    fail: function () {
        console.log('サイト情報の削除に失敗しました。');
    },
    always: function () {
        console.log('サイト情報の削除が完了しました。');
    }
});
```