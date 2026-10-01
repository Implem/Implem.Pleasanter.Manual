---
title: Notification.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: notification-json
translationKey: notification-json
shortname: Notification.json
created: 2019-04-30
updated: 2026-02-10
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 設定値

本パラメータファイルの設定値は下記の通りです。  

|パラメータ名|設定例|説明|
|:--|:--|:--|
|SecurityProtocolType|"Tls12"|TLSのバージョンを指定します。|
|Mail|true|通知種別としてメールの表示有無をtrue/falseで指定します。|
|Slack|true|通知種別としてSlackの表示有無をtrue/falseで指定します。|
|ChatWork|true|通知種別としてChatWorkの表示有無をtrue/falseで指定します。|
|Line|true|通知種別としてLINEおよびLINEグループの表示有無をtrue/falseで指定します。|
|LineWorks|true|通知種別としてLINE WORKSの表示有無をtrue/falseで指定します。|
|Teams|true|通知種別としてMicrosoft Teamsの表示有無をtrue/falseで指定します。|
|Rocket.Chat|true|通知種別としてRocket.Chatの表示有無をtrue/falseで指定します。|
|InCircle|true|通知種別としてInCircleの表示有無をtrue/falseで指定します。|
|HttpClient|true|通知種別としてHttpClientの表示有無をtrue/falseで指定します。|
|CopyWithNotifications|On|通知のコピー設定のデフォルト値を指定します。"On"のときチェックオン、"Off"のときチェックオフ、”Disabled”のとき設定項目を非表示にします。Disabled指定した場合コピーされません。|
|ListOrder|["Mail", "Teams", "Slack"]|通知種別に表示する選択リストの順番を配列形式で指定します。|
|HttpClientEncodings|[ "utf-8", "shift_jis", "euc-jp" ]|エンコーディングプルダウンに表示する選択リストを配列型式で指定します。|

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.2.22.0 以降|InCircleを追加<br>CopyWithNotificationsを追加|
|1.3.7.0 以降|ListOrderを追加|
|1.3.17.0 以降|HttpClientを追加<br>HttpClientEncodingsを追加|
|1.5.1.0 以降|LineWorksを追加|
