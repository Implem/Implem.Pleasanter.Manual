---
title: $p.apiGroupsGet
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-groups-get
translationKey: script-api-groups-get
shortname: $p.apiGroupsGet
created: 2022-07-19
updated: 2026-09-08
---

## 概要

AjaxのPOSTリクエストにより、グループ情報を取得します。

## 構文

### グループIDを直接指定して1件取得する場合

##### JavaScript

```
$p.apiGroupsGet({
    id: <グループID>,
    done: <任意の処理>,
    fail: <任意の処理>,
    always: <任意の処理>
});
``` 

### グループIDを複数指定して取得する場合

##### JavaScript

```
$p.apiGroupsGet({
    data:{
        View: {
            ColumnFilterHash: {
                GroupId: '[<グループIDを配列で指定>]'
            }
        }
    },
    done: <任意の処理>,
    fail: <任意の処理>,
    always: <任意の処理>
});
``` 

## 使用例

### グループIDを直接指定して1件取得する場合

|パラメータ名|説明|必須|
|:--|:--|:--:|
|id|取得対象のグループID|○|
|done|API通信成功|○|
|fail|API通信失敗|-|
|always|完了時|-|

##### JavaScript

```
$p.apiGroupsGet({
    id: 123,
    done: function (data) {
        console.log(data);
        console.log('グループ情報の取得に成功しました。');
    },
    fail: function () {
        console.log('グループ情報の取得に失敗しました。');
    },
    always: function () {
        console.log('グループ情報の取得が完了しました。');
    }
});
``` 

### グループIDを複数指定して取得する場合

|パラメータ名|説明|必須|
|:--|:--|:--:|
|data|取得対象のグループIDを配列で複数指定|○|
|done|API通信成功|○|
|fail|API通信失敗|-|
|always|完了時|-|

##### JavaScript

```
$p.apiGroupsGet({
    data: {
        View: {
            ColumnFilterHash: {
                GroupId: '[100,101]'
            }
        }
    },
    done: function (data) {
        console.log(data);
        console.log('グループ情報の取得に成功しました。');
    },
    fail: function () {
        console.log('グループ情報の取得に失敗しました。');
    },
    always: function () {
        console.log('グループ情報の取得が完了しました。');
    }
});
```
