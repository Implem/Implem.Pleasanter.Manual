---
title: notification
icon: material/alpha-o-box
category: サーバスクリプト
order: '51000'
status: ''
parts: ''
urlstring: server-script-notification
translationKey: server-script-notification
shortname: notification
created: 2021-02-16
updated: 2024-11-12
---

## 概要

生成もしくは取得した通知のオブジェクトを用いて、任意のタイミングで通知を送信することができます。

## プロパティ

|プロパティ|変更|説明|
|:----------|:-------:|:---------------------------|
|Id |○|通知ID|
|Type|○|通知種別(下記「通知種別」参照)|
|Prefix|○|プレフィックス|
|Address|○|送信先アドレス|
|CcAddress|○|Ccに設定する送信先アドレス。Type（通知種別）が"1"（Mail）の場合のみ有効|
|BccAddress|○|Bccに設定する送信先アドレス。Type（通知種別）が"1"（Mail）の場合のみ有効|
|Token|○|トークン|
|UseCustomFormat|○|カスタムデザインを使用|
|Format|○|書式|
|Disabled|○|無効|
|Title|○|タイトル|
|Body|○|内容|

## メソッド

|メソッド|概要|
|:---|:----|
|[Send](server-script-notification-send.md)|通知の送信|

## 通知種別

Type(通知種別)は以下の値が設定可能です。
Mail = 1, Slack = 2, ChatWork = 3, Line = 4, LineGroup = 5, Teams = 6, RocketChat = 7, InCircle = 8
※各通知先ごとに通知に必要なプロパティは異なります。下記マニュアルから通知先ごとの設定を確認してください。
[通知](../../../managers-guide/manage-table/notifications/table-management-notification.md) 「通知種別を指定する」

## 注意事項

こちらは[サーバスクリプト](../index.md)で使用するメソッドです。[スクリプト](../../../managers-guide/manage-table/scripts/index.md)では使用できません。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.10.0 以降|notificationオブジェクトにプロパティCcAddress、BccAddressを追加|

## 関連情報

-   [テーブルの管理：サーバスクリプト](../../../managers-guide/manage-table/server-script/index.md)  
-   [オブジェクトごとの実行タイミング](../basics/server-script-conditions.md)  
-   [notificationsオブジェクト](../notifications/index.md)   
-   [notifications.Newメソッド](../notifications/server-script-notifications-new.md)  
-   [notifications.Getメソッド](../notifications/server-script-notifications-get.md)