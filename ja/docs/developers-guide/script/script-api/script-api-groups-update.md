---
title: $p.apiGroupsUpdate
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-groups-update
translationKey: script-api-groups-update
shortname: ''
created: 2022-07-19
updated: 2026-09-08
---

## 概要

AjaxのPOSTリクエストにより、グループを更新します。

## 構文

##### JavaScript

```
$p.apiGroupsUpdate({
    id: <対象のグループID>,
    data: {
        <更新するグループ情報>
    },
    done: <任意の処理>,
    fail: <任意の処理>,
    always: <任意の処理>
});
``` 

## 各パラメータの説明

|パラメータ名|説明|必須|
|:--|:--|:--:|
|id|更新するグループID|○|
|data|更新するグループ情報　※欄外補足参照|○|
|done|API通信成功|○|
|fail|API通信失敗|-|
|always|完了時|-|

※更新するグループ情報は、[APIグループ更新時](../../api/group-operations/api-group-update.md)と同等のパラメータを設定します。リンク先のマニュアルを参照にパラメータを設定してください。

## 使用例

##### JavaScript

```
$p.apiGroupsUpdate({
    id: 123,
    data: {
        GroupName: '更新後グループ名',
        Body: '更新後グループ内容',
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
        console.log('グループ情報の更新に成功しました。');
    },
    fail: function () {
        console.log('グループ情報の更新に失敗しました。');
    },
    always: function () {
        console.log('グループ情報の更新が完了しました。');
    }
});
```
