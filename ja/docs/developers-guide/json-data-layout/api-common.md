---
title: 共通
category: JSONデータレイアウト
order: '100'
status: ''
parts: ''
urlstring: api-common
translationKey: api-common
shortname: JSONデータレイアウト：共通
created: 2025-02-03
updated: 2026-07-14
---

## 概要

APIやサーバスクリプトでレコードを操作する際に指定するJSON形式のデータレイアウトです。

## JSONデータのレイアウト

|No|プロパティ名|項目名|データ型|備考|
|:----|:----|:----|:----|:----|
|1|ApiVersion|APIのバージョン|long|省略時は[Api.json](../../setup/parameters/api-json.md)の「ApiVersion」で指定したバージョンで動作|
|2|ApiKey|あらかじめ作成した[APIキー](../api/basics/api-key.md)|string|操作するテーブル、操作する内容に応じた権限をもつユーザで作成したAPIキーを設定|
|4|Offset|データ取得するAPIやスクリプトにおいて取得を開始するレコードの位置|long|省略時は0（1件目から取得開始）。[PageSize](../../FAQ/features-for-developers/faq-api-paging.md)の値以降のレコードを取得する場合に設定します。詳細は[FAQ：API で 200 レコードを超えるデータを取得したい](../../FAQ/features-for-developers/faq-api-paging.md)を参照してください。|
|3|PageSize|データ取得するAPIやスクリプトにおいて取得可能な上限値|long|省略時は[Api.json](../../setup/parameters/api-json.md)の[PageSize](../../FAQ/features-for-developers/faq-api-paging.md)で指定した値。[Api.json](../../setup/parameters/api-json.md)のPageSizeよりも大きな値を設定した場合はPageSizeの値として動作します。|

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.13.0 以降|PageSizeを追加|

## 関連情報

-   [パラメータ設定：Api.json](../../setup/parameters/api-json.md)
-   [開発者ガイド：API：APIキーの作成](../api/basics/api-key.md)
-   [FAQ：API で 200 レコードを超えるデータを取得したい](../../FAQ/features-for-developers/faq-api-paging.md)
