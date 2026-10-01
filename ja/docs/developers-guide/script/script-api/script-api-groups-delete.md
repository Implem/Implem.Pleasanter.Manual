---
title: $p.apiGroupsDelete
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-groups-delete
translationKey: script-api-groups-delete
shortname: ''
created: 2022-07-19
updated: 2026-09-08
---

## 概要

AjaxのPOSTリクエストにより、グループを削除します。

## 構文

##### JavaScript

```
$p.apiGroupsDelete ({
    id: <削除対象のグループID>,
    done: <任意の処理>,
    fail: <任意の処理>,
    always: <任意の処理>
});
``` 

## 各パラメータの説明

|パラメータ名|説明|必須|
|:--|:--|:--:|
|id|削除対象のグループID|○|
|done|API通信成功|○|
|fail|API通信失敗|-|
|always|完了時|-|

## 使用例

##### JavaScript

```
$p.apiGroupsDelete({
    id: 123,
    done: function (data) {
        console.log(data);
        console.log('グループ情報の削除に成功しました。');
    },
    fail: function () {
        console.log('グループ情報の削除に失敗しました。');
    },
    always: function () {
        console.log('グループ情報の削除が完了しました。');
    }
});
``` 
