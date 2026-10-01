---
title: BackgroundService.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: background-service-json
translationKey: background-service-json
shortname: BackgroundService.json
created: 2022-05-20
updated: 2026-09-08
---

## 概要

バックグラウンドで実行される機能を設定します。

## 注意事項

- パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。
- `DeleteSysLog`で指定したシステムログの削除が正しく行われない場合は、[こちら](parameter-name-change-deletesyslogs.md)を確認してください。
- `DeleteTrashBox`を有効化（`true`に設定）した場合、削除されたレコードの復元は行えません。誤って重要なデータを削除しないよう、慎重に操作してください。

## 設定値

本パラメータファイルの設定値は下記の通りです。  

| パラメータ名 | 設定例 | 説明 |
| :- | :- | :- |
| EnvironmentVariables | ["Production"] |バックグラウンドサービスを実行する環境を配列形式で設定（複数設定可）。ここで指定した文字列が[Service.json](service-json.md)の DeploymentEnvironment に設定されている環境でのみバックグラウンドサービスが実行される。|
| Reminder | false | リマインダー機能の有効化/無効化をtrue/falseで指定。（リマインダー機能を有効化する際は「[プリザンターのリマインダー機能を有効化する](../additional/notifications/reminder.md)」を参照のこと） |
| ~~ReminderIgnoreConsecutiveExceptionCount~~ | ~~30~~ | ~~リマインダー機能での連続した例外を無視する回数。~~ ※2|
| SyncByLdap | false | LDAP同期を自動実行する機能の有効化/無効化をtrue/falseで指定。有効化には事前に[Authentication.json](authentication-json.md)内のLdapParameters配下のパラメータ設定が必要。 |
| SyncByLdapTime | ["01:00"] | LDAP同期を自動実行する時間。※1 |
| DeleteSysLogs | false | システムログを自動で削除する機能の有効化/無効化をtrue/falseで指定。有効化した場合は[SysLog.json](sys-log-json.md)内のRetentionPeriodパラメータで指定された保存日数を過ぎたシステムログが削除される。 |
| DeleteSysLogsChunkSize | 5000 | 分割削除する場合に一回で削除されるレコード数を指定。分割せずに削除する場合は0を設定。|
| DeleteSysLogsTime | ["02:00"] | システムログの削除を実行する時間。※1 |
| DeleteTemporaryFiles| false | テンポラリファイルを自動で削除する機能の有効化/無効化をtrue/falseで指定。有効化した場合はApp_Data\Temp配下およびApp_Data\Histories配下のファイルが[General.json](general.json.md)内のDeleteTempOldThanとDeleteHistoriesOldThanそれぞれのパラメータで指定された期間を過ぎていた場合に削除される。 |
| DeleteTemporaryFilesTime| ["02:30"] | テンポラリファイルの削除を実行する時間。※1 |
| DeleteTrashBox| false | [ごみ箱](../../users-guide/table/record-authoring/edit-records/table-record-physical-delete.md)内のレコード、およびユーザ/グループ/組織を削除したあとデータベース内の削除済み領域に残るレコードを自動で削除する機能について、有効化/無効化をtrue/falseで指定。※)この機能を有効化した場合、削除されたレコードの復元は行えないため誤って重要なデータを削除しないよう慎重に操作すること。　|
| DeleteTrashBoxTime| ["03:00"] | [ごみ箱](../../users-guide/table/record-authoring/edit-records/table-record-physical-delete.md)内のレコード、および、削除済みユーザ/グループ/組織のレコードの削除を実行する時間。※1 |
| DeleteTrashBoxRetentionPeriod| 90 | [ごみ箱](../../users-guide/table/record-authoring/edit-records/table-record-physical-delete.md)内のレコード、および、削除済みユーザ/グループ/組織のレコードの保存期間を日数で指定する。処理開始時にレコードの更新日時が指定された保存期間より古い場合に削除される。 |
|DeleteUnusedRecord|false|ごみ箱内の削除されたレコードに関連する「未使用の権限」や「リンク情報」を自動的に削除する機能の有効化/無効化をtrue/falseで指定。<br>パラメータDeleteTrashBoxがfalseの場合は、何も削除されないことがある。**本機能による削除は復元を行えない。慎重に設定すること。**|
|DeleteUnusedRecordTime|["03:00"]|未使用の権限やリンク情報の削除を実行する時間。|
|DeleteUnusedRecordChunkSize|1000|未使用の権限やリンク情報を一度に削除する件数。大きな数値を設定すると処理は早く終わるが、サーバに負荷がかかる可能性がある。<br>未設定時または0を設定した場合は、既定値1000が使用される。|
| DeleteMcpLogs | false | MCPログを自動で削除する機能の有効化/無効化をtrue/falseで指定。 |
| DeleteMcpLogsTime | ["02:00"] | MCPログの削除を実行する時間。※1 |
| McpLogsRetentionPeriod| 90 | MCPログの保存期間を日数で指定する。処理開始時に指定された保存期間より更新日時が古い場合に削除される。 |
| DeleteMcpLogsChunkSize | 5000 | MCPログを分割削除する場合に一回で削除されるレコード数を指定。分割せずに削除する場合は0を設定。|

※1 処理開始時間を文字列配列で記述する。24時間表記(HH:mm)。指定した時間に毎日処理が実行される。時間を複数記述することで１日のうち複数回実行させることが可能。記述した時間は[Service.json](service-json.md)のTimeZoneDefaultで指定したタイムゾーンとして扱われる。指定した時間に他の処理が実行中の場合はその処理終了後に実行される。同じ時分を指定した場合の処理開始順は不定。
※2 プリザンター 1.4.7.0以降のバージョンより廃止。リマインダー機能で連続した例外が発生した場合でも処理を中断しない。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.7.0 以降|ReminderIgnoreConsecutiveExceptionCountを追加<br>Reminderを追加|
|1.3.19.0 以降|SyncByLdapTimeを追加<br>SyncByLdapを追加|
|1.3.23.0 以降|DeleteSysLogsTimeを追加<br>DeleteSysLogsを追加|
|1.3.24.0 以降|DeleteTemporaryFilesTimeを追加<br>DeleteTemporaryFilesを追加|
|1.3.25.0 以降|DeleteTrashBoxRetentionPeriodを追加<br>DeleteTrashBoxを追加<br>DeleteTrashBoxTimeを追加|
|1.3.26.0 以降|EnvironmentVariablesを追加|
|1.4.7.0 以降|ReminderIgnoreConsecutiveExceptionCountを削除|
|1.4.16.0 以降|DeleteSysLogsChunkSizeを追加|
|1.5.0.0以降|DeleteUnusedRecordを追加<br>DeleteUnusedRecordTimeを追加<br>DeleteUnusedRecordChunkSizeを追加|
|1.5.2.0以降|DeleteMcpLogs を追加<br>DeleteMcpLogsTime を追加<br>McpLogsRetentionPeriodを追加<br>DeleteMcpLogsChunkSize を追加|