---
title: 大規模環境でリマインダー利用におけるDBの定常負荷を低減する
category: 追加設定：パフォーマンス
order: '500'
status: ''
parts: ''
urlstring: reminder-db-load-reduction
translationKey: reminder-db-load-reduction
shortname: 大規模環境でリマインダー利用におけるDBの定常負荷を低減する
created: 2026-06-01
updated: 2026-06-09
---

## 概要

リマインダーの設定件数・ユーザ数・組織/グループ数が多い大規模環境では、リマインダースケジュールの確認処理がDBの定常負荷の要因になる場合があります。既定の設定では、この確認処理が60秒ごとに起動します。

バージョン1.5.5.0以降では、[BackgroundService.json](../../parameters/background-service-json.md)のReminderCheckIntervalSecondsパラメータで起動間隔（単位：秒）を変更できます。日次以上の頻度で運用するリマインダーでは、起動間隔を120〜300秒に延長しても実用上の即時性は維持されます。

## 制限事項

1. [BackgroundService.json](../../parameters/background-service-json.md)のReminderCheckIntervalSecondsに設定できる値の範囲は30〜3600（秒）です。範囲外の値を指定した場合は、自動的に最も近い有効値に変更して動作します。

   |指定値|実際の動作|
   |:--|:--|
   |10（下限未満）|30として動作|
   |7200（上限超過）|3600として動作|

   有効値への変更を行った場合、「[システムログ](../../../managers-guide/system-log-administration/index.md)」へ以下のような警告メッセージが記録されます。

   ``` text
   "ReminderCheckIntervalSeconds is out of range. Configured: 7200, Used: 3600 (valid range: 30-3600)."
   ```

1. 起動間隔を延長すると、リマインダーの送信タイミングが最大で設定値の秒数だけ遅延します。分単位の即時性が必要なリマインダー運用には適しません。
1. [Reminder.json](../../parameters/reminder-json.md)のInterval（処理ごとの待機時間）および Span（1回の起動内でのループ継続秒数）は、本ページで説明する起動間隔とは独立したパラメータです。これらの調整のみでは起動頻度に起因する負荷は低減されません。
1. 最適な設定値はサーバの性能・負荷状況に依存します。以下の設定例はあくまでも目安です。

## 設定例

##### BackgroundService.json（関連パラメータのみを抜粋）

```json
{
    "Reminder": true,
    "ReminderCheckIntervalSeconds": 120
}
```

## 対応バージョン

| 対応バージョン | 内容 |
| :-- | :-- |
| 1.5.5.0以降 | 機能追加 |
