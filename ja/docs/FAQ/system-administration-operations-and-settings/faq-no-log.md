---
title: 特定のIPアドレスからのアクセスログをSysLogsテーブルに記録しないようにしたい
category: FAQ：システム管理の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-no-log
translationKey: faq-no-log
shortname: ''
created: 2020-08-01
updated: 2024-04-29
---

## 回答

パラメータ[SysLog.json](../../setup/parameters/sys-log-json.md)の「NotLoggingIp」を設定してください。

---

## 概要

プリザンターはシステムログをデータベースのSysLogsテーブルへ記録しています。監視システム等をご利用の際はSysLogsテーブルの大半をそのアクセスログで占める可能性があります。監視システム等からのアクセスログを記録しないようにするためにはパラメータ[SysLog.json](../../setup/parameters/sys-log-json.md)の「NotLoggingIp」に監視システムなどログ記録を抑止したいシステムのIPアドレスを設定してください。

## 操作方法

1.  Parametersフォルダ配下のSysLog.jsonファイルを開きます。
1.  NotLoggingIp項目へ以下のように配列形式でIPアドレスを入力します。複数のIPアドレスを入力する際はカンマ区切りで記入します。

    ``` json linenums="1"
    {
        "RetentionPeriod": 90,
        "NotLoggingIp":[ "10.10.10.10", "10.10.10.20" ]
    }
    ```

1.  Webサーバ、またはプリザンターを再起動します。
1.  SysLogsテーブルを開き、2で設定したIPアドレスからのアクセスログが記録されていないことを確認します。

## 関連情報

-   [パラメータ設定：SysLog.json](../../setup/parameters/sys-log-json.md)
