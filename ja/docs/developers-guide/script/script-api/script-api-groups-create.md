---
title: $p.apiGroupsCreate
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-groups-create
translationKey: script-api-groups-create
shortname: ''
created: 2022-07-19
updated: 2026-09-08
---

## 概要

AjaxのPOSTリクエストにより、グループを作成します。

## 構文

##### JavaScript

```
$p.apiGroupsCreate({
    data: {
        <作成するグループ情報>
    },
    done: <任意の処理>,
    fail: <任意の処理>,
    always: <任意の処理>
});
``` 

## 各パラメータの説明

|パラメータ名|説明|必須|
|:--|:--|:--:|
|data|作成するグループ情報　※欄外補足参照|-|
|done|API通信成功|○|
|fail|API通信失敗|-|
|always|完了時|-|

※作成するグループ情報は、[APIグループ作成時](../../api/group-operations/api-group-create.md)と同等のパラメータを設定します。リンク先のマニュアルを参照にパラメータを設定してください。

## 使用例

##### JavaScript

```
$p.apiGroupsCreate({
    data: {
        GroupName: '作成グループ名',
        Body: '作成グループ内容',
        GroupMembers: [
            'User,1,True',
            'Dept,1,False'
        ],
        "GroupChildren": [
            "Group,1,"
        ]
    },
    done: function (data) {
        console.log(data);
        console.log('グループ情報の作成に成功しました。');
    },
    fail: function (data) {
        console.log('グループ情報の作成に失敗しました。');
    },
    always: function (data) {
        console.log('グループ情報の作成が完了しました。');
    }
});
```
