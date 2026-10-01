---
title: 機能概要
category: 開発支援ツール
order: '1000'
status: ''
parts: ''
urlstring: development-tools-overview
translationKey: development-tools-overview
shortname: Pleasanter Extensions,Development Tools,機能概要
created: 2025-01-27
updated: 2025-02-14
---

## 概要

本ソフトウェアは、プリザンターの開発者向けにスクリプトやCSSなどソースコードのアップロード機能、サイト設定の移行機能等を提供します。各機能はプリザンターのWebサーバを経由せずSQL ServerまたはPostgreSQLに直接アクセスし動作します。

![Development Tools の画面例](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/development-tools/assets/c1de2d2bde8044e4871fb101501be416.png)

## バージョン

2.0.0

## 動作環境

本ソフトウェアは下記の環境で動作します。.NET8 SDKは事前にインストールしてください。

- Windows 10 / 11
- .NET8 SDK

## 制限事項

1. 本ソフトウェアはデータベースに直接アクセスして動作します。Pleasanter.netなどデータベースへの接続を許可されていない環境では使用できません。
1. 本ソフトウェアを使用するには年間サポートサービスの契約時に提供されるEnterprise Editionのライセンスが必要です。

## 機能一覧

本ソフトウェアは下記の機能を提供します。

### Codesメニュー

|機能名|概要|
|---|---|
|Get SiteSettings codes|特定の[サイトからソースコードを取得](development-tools-get-sitesettings-codes.md)します|
|Upload SiteSettings codes|特定の[サイトにソースコードをアップロード](development-tools-upload-sitesettings-codes.md)します|

### Extensionsメニュー

|機能名|概要|
|---|---|
|Get Extensions|[Extensionsテーブルからソースコードを取得](development-tools-get-extensions.md)します|
|Upload Extensions|[Extensionsテーブルへソースコードをアップロード](development-tools-upload-extensions.md)します|

### Sitesメニュー

|機能名|概要|
|---|---|
|Convert SiteSettings|[サイト設定の移行](development-tools-convert-sitesettings.md)をします|
|Get SiteSettings histories|[サイト設定の変更履歴](development-tools-get-sitesettings-histories.md)を取得します|

### UserSQLメニュー

|機能名|概要|
|---|---|
|Execute SQL|[SQLでレコードを抽出](development-tools-execute-sql.md)します|
|Open folder: CSV|[抽出したレコードをCSV形式で出力](development-tools-open-csv-folder.md)します|

## 関連情報

-   [Development Tools：特定のサイトからソースコードを取得する](development-tools-get-sitesettings-codes.md)
-   [Development Tools：特定のサイトにソースコードをアップロードする](development-tools-upload-sitesettings-codes.md)
-   [Development Tools：Extensionsテーブルからソースコードを取得する](development-tools-get-extensions.md)
-   [Development Tools：Extensionsテーブルへソースコードをアップロードする](development-tools-upload-extensions.md)
-   [Development Tools：サイト設定の移行](development-tools-convert-sitesettings.md)
-   [Development Tools：サイト設定の変更履歴を取得する](development-tools-get-sitesettings-histories.md)
-   [Development Tools：SQLでレコードを抽出する](development-tools-execute-sql.md)
-   [Development Tools：抽出したレコードをCSV形式で出力する](development-tools-open-csv-folder.md)
