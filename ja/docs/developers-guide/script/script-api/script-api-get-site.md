---
title: $p.apiGetSite
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-get-site
translationKey: script-api-get-site
shortname: $p.apiGetSite
created: 2022-07-05
updated: 2025-10-06
---

## 概要

AjaxのPOSTリクエストにより、[サイト](../../../users-guide/site/index.md)情報を取得します。

## 構文

##### JavaScript

```
$p.apiGetSite({
    id: <取得対象のサイトID>,
    done: <任意の処理>,
    fail: <任意の処理>,
    always: <任意の処理>
});
``` 

## 各パラメータの説明

|パラメータ名|説明|必須|
|:--|:--|:--:|
|id|取得対象のサイトID|○|
|done|API通信成功|○|
|fail|API通信失敗|-|
|always|完了時|-|

## 使用例

##### JavaScript

```
$p.apiGetSite({
    id: 123,
    done: function (data) {
        console.log(data);
        console.log('サイト情報の取得に成功しました。');
    },
    fail: function () {
        console.log('サイト情報の取得に失敗しました。');
    },
    always: function () {
        console.log('サイト情報の取得が完了しました。');
    }
});
```

## 関連情報

-   [サイト機能](../../../users-guide/site/index.md)
