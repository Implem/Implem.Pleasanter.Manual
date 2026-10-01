---
title: BackgroundService.json設定ファイル内のパラメータ名DeleteSysLogsおよびDeleteSysLogsTime変更について
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: parameter-name-change-deletesyslogs
translationKey: parameter-name-change-deletesyslogs
shortname: DeleteSysLogのパラメータ名変更
created: 2022-10-12
updated: 2023-04-05
---

## 概要

バージョン1.3.23.0において追加された[BackgroundService.json](background-service-json.md)ファイル内のパラメータの一部がバージョン1.3.24.0で変更となりました。

バージョン1.3.23.0から1.3.24.0以降のバージョンへ移行する場合は、以下の通りパラメータの値の転記が必要となります。

| No. | 変更前<br>（1.3.23.0でのパラメータ名） | 変更後<br>（1.3.24.0以降でのパラメータ名） |
| --: | :------------------------------------- | :----------------------------------------- |
|   1 | DeleteSysLog                           | DeleteSysLogs                              |
|   2 | DeleteSysLogTime                       | DeleteSysLogsTime                          |

## 関連情報

-   [パラメータ設定：BackgroundService.json](background-service-json.md)