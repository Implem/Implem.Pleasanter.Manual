---
title: Reminder.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: reminder-json
translationKey: reminder-json
shortname: Reminder.json
created: 2019-04-30
updated: 2026-02-10
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 設定値

本パラメータファイルの設定値は下記の通りです。  

|パラメータ名|設定例|説明|
|:--|:--|:--|
|Enabled|true|リマインダー機能の有効化/無効化をtrue/falseで指定。|
|Mail|false|リマインダーの種別でメールの有効化/無効化をtrue/falseで指定。|
|Slack|false|リマインダーの種別でSlackの有効化/無効化をtrue/falseで指定。|
|ChatWork|false|リマインダーの種別でChatWorkの有効化/無効化をtrue/falseで指定。|
|Line|false|リマインダーの種別でLINEの有効化/無効化をtrue/falseで指定。|
|LineWorks|false|リマインダーの種別でLINE WORKSの有効化/無効化をtrue/falseで指定。|
|Teams|false|リマインダーの種別でTeamsの有効化/無効化をtrue/falseで指定。|
|RocketChat|false|リマインダーの種別でRocket.Chatの有効化/無効化をtrue/falseで指定。|
|InCircle|false|リマインダーの種別でInCircleの有効化/無効化をtrue/falseで指定。|
|Interval|500|リマインダーの時刻監視をサーバサイドで継続的に再実行するまでのインターバルをミリ秒単位で指定。|
|Span|30|リマインダーの時刻監視をサーバサイドで継続的に再実行するか判断するための経過時間を秒単位で指定。|
|Limit|1000|リマインダーで送付するレコード件数の上限を指定。|
|DefaultLine|[Title] --- [Owner] ([Status])|リマインダーに表示するレコードの書式を指定。[Title]等の記述は各項目の内容に置換。|
|MinRange|1|リマインダーの範囲で指定可能な最小値を設定。|
|MaxRange|1000|リマインダーの範囲で指定可能な最大値を設定。|
|DefaultRange|30|リマインダーの範囲の既定値を設定。|
|CopyWithReminders|On|リマインダーのコピー設定のデフォルト値を指定します。"On"のときチェックオン、"Off"のときチェックオフ、”Disabled”のとき設定項目を非表示にします。Disabled指定した場合コピーされません。|
|ListOrder|[ "Mail", "InCircle", "Slack", "ChatWork", "Line", "LineGroup", "Teams", "RocketChat" ]|通知先の一覧の表示順序を設定。nullの場合はデフォルトの順序で表示。|

## 対応バージョン

|対応バージョン|内容|
|-|-|
|1.5.1.0|LineWorksを追加|
