---
title: groups
icon: material/alpha-o-box
category: サーバスクリプト
order: '30000'
status: ''
parts: ''
urlstring: server-script-groups
translationKey: server-script-groups
shortname: groups,groups.Get,groups.Update
created: 2021-06-08
updated: 2026-09-08
---

## 概要

[サーバスクリプト](../index.md)で使用可能な「groupオブジェクト」の操作を行うオブジェクトです。

## メソッド

|No|Name|Description|
|:---|:---|:---|
|1|[Create](server-script-groups-create.md)|「[サーバスクリプト](../index.md)」から新しいグループを作成します。|
|2|[Get](server-script-groups-get.md)|指定したグループIDのグループ情報を取得します。|
|3|[Update](server-script-groups-update.md)|指定したグループを更新します。|

## 使用例

下記の例ではグループID 1 のグループ名をログに出力します。

##### JavaScript

```
let group = groups.Get(1);
if (group) {
    context.Log(group.GroupName);
}
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)