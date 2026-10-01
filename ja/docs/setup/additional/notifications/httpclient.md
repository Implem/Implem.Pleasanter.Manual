---
title: HTTPクライアントで通知できるように設定する
category: 追加設定：通知
order: '900'
status: ''
parts: ''
urlstring: httpclient
translationKey: httpclient
shortname: HttpClient
created: 2022-08-03
updated: 2025-01-30
---

## 概要

HTTPクライアントを使って任意のリクエストを送ることができます。

![HTTPクライアントによる通知の設定画面](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/d0221afd695746fb81b81d2c0f9410de.png)

## 注意事項

1. リクエスト先URL(アドレス欄)は固定になります。
2. Cookieは使えません

## 前提条件

1. [Notification.json](../../parameters/notification-json.md)の「HttpClient」をtrueに設定してください。

## 設定項目

|項目名|必須|概要|
|:--|:-:|:--|
|アドレス|○|リクエスト先のURLを入力してください。|
|メソッド種別|-|HTTPリクエストメソッドを指定します。GET,POST,PUT,DELETEが指定できます。既定値はGETです。|
|エンコーディング|-|通知内容の文字エンコーディングを指定します。utf-8,shift_jis,euc-jpが指定できます。既定値はutf-8です。[Notification.json](../../parameters/notification-json.md)のHttpClientEncodingsでプルダウンの選択肢を指定できます。|
|メディア種別|-|通知内容のメディアタイプ(Content-Type)を指定します。既定値はapplication/jsonです。|
|HTTPヘッダ|-|追加のHTTPヘッダをJSON型式で指定してください。例) {"User-Agent":"Mozilla/5.0 .."}|

## 対応バージョン

|バージョン|内容|
|:--|:--|
|1.3.17.0 以降|機能追加|
