---
title: SysLog.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: sys-log-json
translationKey: sys-log-json
shortname: SysLog.json
created: 2019-04-30
updated: 2026-08-18
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 設定値

本パラメータファイルの設定値は下記の通りです。  

|パラメータ名|設定例|説明|
|:--|:--|:--|
|RetentionPeriod|90|SysLogsテーブルに格納されるシステムログの保存日数を指定します。バックグラウンドタスクを実行すると記載の日数より古いシステムログを削除します。0を指定した場合には無期限となります。|
|NotLoggingIp|[ "10.10.10.10", "10.10.10.20", "10.10.1.0/24" ]|システムログに記録しないIPアドレスを指定します。監視システムからのアクセス等に使用します。指定方法は、IPアドレスによる表記およびCIDR表記による指定が可能です。|
|LoginSuccess|true|ログイン成功時のシステムログの記録要否をtrue/falseで設定します。|
|LoginFailure|true|ログイン失敗時のシステムログの記録要否をtrue/falseで設定します。|
|SignOut|true|ログアウト時のシステムログの記録要否をtrue/falseで設定します。|
|ClientId|true|trueにすると、操作しているクライアントを識別するClientIdをCookieに保存します。ログイン、ログアウト時にそのClientIdをシステムログに記録します。|
|ExportLimit|1000|[システムログ管理機能](../../managers-guide/system-log-administration/index.md)でエクスポートするシステムログの件数を設定します。|
|EnableLoggingToDatabase|true|システムログをデータベースに記録するかどうかを設定します。|
|EnableLoggingToFile|false|システムログをファイルに記録するかどうかを設定します。|
|OutputErrorDetails|true|trueにすると、ErrStackTrace項目に更に詳細なエラー情報が出力します。|

システムログをファイルに記録する詳細につきましては、[システムログのテキスト出力](../additional/ops-management/syslogs-text-output.md)を参照してください。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.16.0 以降|OutputErrorDetailsを追加|

## 関連情報

-   [パラメータ設定：パラメータ変更時の確認事項](parameter-edit.md)
-   [システムログ管理機能](../../managers-guide/system-log-administration/index.md)
-   [システムログをテキスト出力できるようにする](../additional/ops-management/syslogs-text-output.md)
