---
title: プリザンターのリマインダー機能を有効化する
category: 追加設定：通知
order: '200'
status: ''
parts: ''
urlstring: reminder
translationKey: reminder
shortname: リマインダー
created: 2019-04-29
updated: 2026-06-09
---

## 概要

[リマインダー](../../../users-guide/hands-on/advanced/advanced-operations-notification.md)機能を有効化する方法を説明します。ご利用のプリザンターのバージョンが1.3.7以降の場合に本手順でリマインダー機能を有効化してください。

## 制限事項

1. プリザンターのバージョン 1.3.7.0 以降、リマインダーを有効化する手順が変更になりました。ご利用環境が以下に当てはまる場合は「プリザンターのリマインダー機能を有効化する（外部スクリプト）」を確認してください。  

    -   ご利用のプリザンターのバージョンが1.3.6以前である    
    -   統合Windows認証を有効とした環境である（バージョン問わず）   

1. 本手順の設定をしたまま、「プリザンターのリマインダー機能を有効化する（外部スクリプト）」の手順で設定するとリマインダーが二重起動し、メールが複数回送信される可能性があります。

## 操作手順

[BackgroundService.json](../../parameters/background-service-json.md)および[Service.json](../../parameters/service-json.md)のパラメータ設定値を変更してください。なお、パラメータ変更時はマニュアル[パラメータ変更時の確認事項](../../parameters/parameter-edit.md)を確認してください。

#### BackgroundService.json

マニュアル「[パラメータ設定：BackgroundService.json](../../parameters/background-service-json.md)」を参照し、BackgroundService.jsonファイル内の設定を下記の設定値に変更してください。

|項目|設定例|説明|
|:--|:--|:--|
|Reminder|true|リマインダー機能の有効化|

#### Service.json

マニュアル「[パラメータ設定：Service.json](../../parameters/service-json.md)」を参照し、Service.jsonファイル内の設定を下記の設定値に変更してください。

|項目|設定例|説明|
|:--|:--|:--|
|AbsoluteUri|"http://pleasanter.example.local"|通知やリマインダーに記載されるURLの先頭部分を記入してください。(nullは使えません。)|

## 関連情報

-   [応用編：通知、リマインダー](../../../users-guide/hands-on/advanced/advanced-operations-notification.md)
-   [パラメータ設定：BackgroundService.json](../../parameters/background-service-json.md)
-   [パラメータ設定：Service.json](../../parameters/service-json.md)
-   [パラメータ設定：パラメータ変更時の確認事項](../../parameters/parameter-edit.md)
