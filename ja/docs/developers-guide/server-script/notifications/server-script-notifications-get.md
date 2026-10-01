---
title: notifications.Get
icon: material/alpha-m-box
category: サーバスクリプト
order: '50000'
status: ''
parts: ''
urlstring: server-script-notifications-get
translationKey: server-script-notifications-get
shortname: notifications.Get
created: 2021-02-16
updated: 2023-07-05
---

## 概要

対象テーブルに設定されている通知の情報を取得することができます。

## 構文

```
notifications.Get(id)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|id|int|○|通知のIDを指定|

## 戻り値

通知の設定を取得できたらtrue、取得できなかったらfalseを返却します。

## 使用例

以下の例では、通知IDが2の設定を取得し、IDとアドレスをログに出力します。

##### JavaScript

```
let notification = notifications.Get(2);
context.Log(`${notification.Id},${notification.Address}`);
```

## 注意事項

こちらは[サーバスクリプト](../index.md)で使用するメソッドです。[スクリプト](../../../managers-guide/manage-table/scripts/index.md)では使用できません。

## 関連情報

-   [テーブルの管理：サーバスクリプト](../../../managers-guide/manage-table/server-script/index.md)  
-   [オブジェクトごとの実行タイミング](../basics/server-script-conditions.md)  
-   [notificationsオブジェクト](index.md)   
-   [notificationオブジェクト](../notification/index.md)  
-   [notifications.Newメソッド](server-script-notifications-new.md)